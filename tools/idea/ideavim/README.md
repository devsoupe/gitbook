---
description: IdeaVIM을 정리한 내용입니다.
---

# IdeaVIM

ideavim

vim-easymotion

acejump

vim-extension



\
Next tab: g + t

Prior tab: g + T

Numbered tab: _nnn +_ g + t\
\
\
임시복붙

```
y - yank
i - inner
p - paragraph
```



<pre><code>va{Vy
<strong>
</strong><strong>Place the cursor somewhere in my method,
</strong>va{ to visually select the the code block,
V to turn the selection from character-wise to line-wise,
y to yank
</code></pre>



```
nnoremap <silent> yam ]m{jV]m%y
This maps the keybinding yam (yank a method), which will work from anywhere inside the function body. It works as follows:

]m : goto the start of the function declaration
{j : move right above one paragraph up then move down one line, this helps with multiline function declarations. { will work as long as your function declaration has no empty lines inside of it.
V]m : start visually selecting (line-wise) and then move your cursor to the opening bracket of the function body
%y : move your cursor to the closing bracket of the function body, then yank
```



```
nnoremap <silent> dam ]m{jV]m%x
```





