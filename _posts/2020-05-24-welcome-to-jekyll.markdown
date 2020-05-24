---
layout: post
title:  Look, a post
date:   2020-05-24 15:09:13 +1000
categories: jekyll update
---

Oh look a post. So why did I choose to use jekyll?

Short answer: because html is a bore.

To test things out, below is an elisp hack for collecting slime/sly's fasls into a single directory.

{% highlight lisp %}
(defvar *my-fasldir* "fasl/")

(defun my-sly-compile-file ()
  (interactive)
  (let* ((rootdir (projectile-project-root))
         (fasldir (concat (projectile-project-root) *my-fasldir*))
         (relative-dir (string-trim-right
                        (substring (buffer-file-name (current-buffer)) (length rootdir))
                        "[^/]+"))
         (file-fasl-dir (concat fasldir relative-dir)))
    (make-directory file-fasl-dir t)
    (setq sly-compile-file-options (list :fasl-directory file-fasl-dir))
    (sly-compile-file)))

; if using use-package do
; :bind (:map sly-editing-mode-map ("C-c C-k" . #'my-sly-compile-file))
; otherwise
(bind-key "C-c C-k" #'my-sly-compile-file sly-editing-mode-map)
{% endhighlight %}
