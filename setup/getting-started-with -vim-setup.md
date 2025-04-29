# Quick Vim Setup for Kubernetes Exams

In high-pressure Kubernetes certification exams like **CKA**, **CKAD**, or **CKS**, setting up your Vim environment efficiently can save precious time. This guide summarizes tips shared by the community to improve your editing workflow during the exam.

---

## 🧠 Why Configure Vim in the Exam?

By default, Vim in the exam environment may not have:

- Line numbers
- Syntax highlighting
- Proper YAML indentation

A few quick settings can help:

- Avoid indentation mistakes
- Navigate YAML more easily
- Speed up editing with better visuals

---

## ⚙️ Recommended `.vimrc` Configuration

Create or update your `.vimrc` file with the following content:

```bash
cat <<EOF > ~/.vimrc
set number
set tabstop=2
set shiftwidth=2
set expandtab
syntax on
EOF
```

### What these settings do:

- `set number`: Show line numbers
- `set tabstop=2`: Set tab width to 2 spaces
- `set shiftwidth=2`: Auto-indent width
- `set expandtab`: Convert tabs to spaces
- `syntax on`: Enable syntax highlighting

---

## ⚡ One-Liner Setup

For quicker setup, run this one-liner:

```bash
echo -e "set number\nset tabstop=2\nset shiftwidth=2\nset expandtab\nsyntax on" > ~/.vimrc
```

---

## 💡 Temporary Settings (No `.vimrc`)

If you're unable to create or use `.vimrc`, you can apply settings directly inside Vim:

```vim
:set number
:set ts=2
:set sw=2
:set expandtab
:syntax on
```

---

## ✅ Validation

Open a test YAML file to verify the settings:

```bash
vim test.yaml
```

You should see line numbers, proper indentation, and syntax highlighting.

---

## 📚 References

- [KodeKloud Community Discussion](https://kodekloud.com/community/t/curious-are-there-any-tips-for-getting-vim-setup-quickly-in-the-exam-to-help-av/222894)
- [CKA Certification Guide](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/)

---

Happy Learning, and good luck with your exam! 🚀