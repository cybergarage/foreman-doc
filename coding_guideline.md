![foreman_logo](./img/icon.png)

# Coding Guidelines

This document aims to describe an introduction to Foreman committers and contributors.
To develop `foreman-go` and `foreman-cc`, you should understand the following coding guidelines.

## Go

To develop `foreman-go`, you must follow the following coding guidelines basically.

- [Effective Go](https://golang.org/doc/effective_go.html#interface-names)

### Extra Coding Guideline

In addition to the above standard guideline, you must follow the following extra rules too.

#### Interface names

[Effective Go](https://golang.org/doc/effective_go.html#interface-names) specifies only an interface naming rule when the interface has only a method. 
Multiple-method interfaces are named by the class name plus an `-ing` suffix.

## C++

To develop `foreman-cc`, you must follow understand the following coding guidelines basically.

- [WebKit Code Style Guidelines](https://webkit.org/code-style-guidelines/)

We extends the standard guideline, and the all source codes of `foreman-cc` are formatted automatically by `clang-format` based on the following setting.

- [.clang-format](https://github.com/cybergarage/foreman-cc/blob/master/.clang-format)