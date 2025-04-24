This is an experiment to show that the css tailwind generates will look a little different
than what we had in our scss. If you look at [output.css](output.css), you'll see the main
differences are that:
* it puts everything in a `@layer utilities`,
* it uses `var` for any spacing units,
* and it uses `(padding|margin)-(inline|block`) instead of `left/right` (as I explain below)

We may want to consider copy/pasting the output.css of this
verbatim as our temporary "pat" prefixed css, so that when we tell people to delete the
prefix, it does exactly the same thing as it was.

run this with `npm i && npx @tailwindcss/cli -i ./input.css -o ./output.css --watch`

## Notes on differences:

The css generated for margins and padding looks a little different than what we had,
since it uses `calc` and `var`s, but shouldn't be a problem
```css
// for example, ours looked like:
.m-2 {
  margin: 8px;
}
// tailwind's looks like
.m-2 {
  margin: calc(var(--spacing) * 2);
}
```

Additionally,  for `.my-*`, `.py-*` classes,
tailwind uses `margin-block` and `padding-block` while we use `margin-top` + `margin-bottom` and `padding-top` + `padding-bottom`

And for `.mx-*` and `px-*` classes, tailwind uses `margin-inline` and `padding-inline` while
we use `margin-left` + `margin-right` and `padding-left` + `padding-right`.

This shouldn't be a problem but I just wanted to make sure we were aware of the difference.
```css
// for example, ours looked like:
.mx-2 {
  margin-left: #{$original}px;
  margin-right: #{$original}px;
}
// tailwind's looks like
.mx-2 {
  margin-inline: calc(var(--spacing) * 2);
}
```


since tailwind looks for tokens _anywhere_ in your source
(they don't need to be in class="" attributes or anything like that),
we just spit them all out here so they get put put into output.css

```
m-0 -> pat:m-0 (no change)
m-2 -> pat:m-0.5 (Tailwind's 0.5 = 2px)
m-4 -> pat:m-1 (Tailwind's 1 = 4px)
m-8 -> pat:m-2 (Tailwind's 2 = 8px)
m-10 -> pat:m-2.5 (Tailwind's 2.5 = 10px)
m-16 -> pat:m-4 (Tailwind's 4 = 16px)
m-20 -> pat:m-5 (Tailwind's 5 = 20px)
m-24 -> pat:m-6 (Tailwind's 6 = 24px)
m-32 -> pat:m-8 (Tailwind's 8 = 32px)
m-40 -> pat:m-10 (Tailwind's 10 = 40px)
m-48 -> pat:m-12 (Tailwind's 12 = 48px)
m-56 -> pat:m-14 (Tailwind's 14 = 56px)
m-64 -> pat:m-16 (Tailwind's 16 = 64px)
m-72 -> pat:m-18 (Tailwind's 18 = 72px)



pat:mx-0
pat:mx-0.5
pat:mx-1
pat:mx-2
pat:mx-2.5
pat:mx-4
pat:mx-5
pat:mx-6
pat:mx-8
pat:mx-10
pat:mx-12
pat:mx-14
pat:mx-16
pat:mx-18

pat:my-0
pat:my-0.5
pat:my-1
pat:my-2
pat:my-2.5
pat:my-4
pat:my-5
pat:my-6
pat:my-8
pat:my-10
pat:my-12
pat:my-14
pat:my-16
pat:my-18

pat:mt-0
pat:mt-0.5
pat:mt-1
pat:mt-2
pat:mt-2.5
pat:mt-4
pat:mt-5
pat:mt-6
pat:mt-8
pat:mt-10
pat:mt-12
pat:mt-14
pat:mt-16
pat:mt-18

pat:mr-0
pat:mr-0.5
pat:mr-1
pat:mr-2
pat:mr-2.5
pat:mr-4
pat:mr-5
pat:mr-6
pat:mr-8
pat:mr-10
pat:mr-12
pat:mr-14
pat:mr-16
pat:mr-18

pat:mb-0
pat:mb-0.5
pat:mb-1
pat:mb-2
pat:mb-2.5
pat:mb-4
pat:mb-5
pat:mb-6
pat:mb-8
pat:mb-10
pat:mb-12
pat:mb-14
pat:mb-16
pat:mb-18

pat:ml-0
pat:ml-0.5
pat:ml-1
pat:ml-2
pat:ml-2.5
pat:ml-4
pat:ml-5
pat:ml-6
pat:ml-8
pat:ml-10
pat:ml-12
pat:ml-14
pat:ml-16
pat:ml-18




pat:p-0
pat:p-0.5
pat:p-1
pat:p-2
pat:p-2.5
pat:p-4
pat:p-5
pat:p-6
pat:p-8
pat:p-10
pat:p-12
pat:p-14
pat:p-16
pat:p-18

pat:px-0
pat:px-0.5
pat:px-1
pat:px-2
pat:px-2.5
pat:px-4
pat:px-5
pat:px-6
pat:px-8
pat:px-10
pat:px-12
pat:px-14
pat:px-16
pat:px-18

pat:py-0
pat:py-0.5
pat:py-1
pat:py-2
pat:py-2.5
pat:py-4
pat:py-5
pat:py-6
pat:py-8
pat:py-10
pat:py-12
pat:py-14
pat:py-16
pat:py-18

pat:pt-0
pat:pt-0.5
pat:pt-1
pat:pt-2
pat:pt-2.5
pat:pt-4
pat:pt-5
pat:pt-6
pat:pt-8
pat:pt-10
pat:pt-12
pat:pt-14
pat:pt-16
pat:pt-18

pat:pr-0
pat:pr-0.5
pat:pr-1
pat:pr-2
pat:pr-2.5
pat:pr-4
pat:pr-5
pat:pr-6
pat:pr-8
pat:pr-10
pat:pr-12
pat:pr-14
pat:pr-16
pat:pr-18

pat:pb-0
pat:pb-0.5
pat:pb-1
pat:pb-2
pat:pb-2.5
pat:pb-4
pat:pb-5
pat:pb-6
pat:pb-8
pat:pb-10
pat:pb-12
pat:pb-14
pat:pb-16
pat:pb-18

pat:pl-0
pat:pl-0.5
pat:pl-1
pat:pl-2
pat:pl-2.5
pat:pl-4
pat:pl-5
pat:pl-6
pat:pl-8
pat:pl-10
pat:pl-12
pat:pl-14
pat:pl-16
pat:pl-18



pat:gap-1
pat:gap-2
pat:gap-4

pat:delay-0
pat:delay-50
pat:delay-100
pat:delay-150
pat:delay-200
pat:delay-250
pat:delay-300
pat:delay-350
pat:delay-400
pat:delay-450
pat:delay-500
pat:delay-1000

```

#### a note on `pat:` vs `pat-` prefix:
To use `pat` as the prefix in this, I passed `prefix(pat)` in [input.css](input.css),
and [in the new version of tailwind (v4), prefixes use a colon `:` instead of a dash `-`](https://tailwindcss.com/docs/upgrade-guide#:~:text=Prefixes%20now%20look%20like%20variants).
So if we wanted to use `pat:` as our temporary prefix, we can copy/paste output.css verbatim,
otherwise I'd recommend removing the `prefix(pat)` from input.css, regenerating output.css,
and then manually adding a `pat-` in front of each style rule in output.css.
