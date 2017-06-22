# Accelerated TensorFlow development with packages

Software package managers such as Homebrew, apt, and rpm let
developers quickly install and use software. They provide an essential
role in accelerating software development through component reuse. Is
it possible to apply similar patterns and tooling to TensorFlow
development? In this talk, Garrett Smith, project lead of Guild AI,
will present a specification for code reuse in TensorFlow that
includes pre-trained models, datasets, and project templates. He'll
demonstrate Guild's packaging command set, which can be used to build,
deploy, and install TensorFlow packages, saving developers time
getting started with their projects.

## Outline


- Max OS, Windows, Linux - setup for "package managers"
- What is a package management system?
  - Source code
  - Build scripts - make it easy to compile source to binaries
  - Precompiled binaries
  - Package descriptor
  - Package container (tar file)
  - Repository of packages (search and download)
  - Tools for installing, upgrading, uninstalling (end user)
  - Tools for creating and publishing packages (package maintainer)
- Flow of knowledge: research, code, users
