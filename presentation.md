## Accelerated TensorFlow development with packages

TensorFlow Chicago - June 22, 2017

[Garrett Smith](http://gar1t.com) / [@gar1t](https://twitter.com/gar1t)

<a href="https://guild.ai">
<img src="img/logo-white-lg.png" width="200" style="margin-top:2rem">
</a>

---

## Topics

<ul>
<li class="fragment">High level work flows
<li class="fragment">Guild packages
<li class="fragment">Live demo
</ul>

---

<img src="img/role1.png">

---

<img src="img/role2.png">

---

<img src="img/role3.png">

---

<img src="img/role4.png">

---

<img src="img/role5.png">

---

<img src="img/role6.png">

---

<img src="img/role7.png">

---

<img src="img/role9.png">

---

<img src="img/role8.png">

---

<img src="img/role10.png">

---

## Packaging is everywhere!

- All major Linux distros
- Bower (web front-end libraries)
- Homebrew (MacOS)
- npm (Node)
- Gem (Ruby)
- Pip (Python)
- Conda (Anaconda)

---

## Guild packages

<ul>
<li class="fragment">Tools for *TensorFlow package maintainers*
<li class="fragment">Modeled off system packaging workflow
<li class="fragment">Pre-release but usable
</ul>

---

## Goals

<ul>
<li class="fragment">Standardize discovery and use of TensorFlow models and supporting code
<li class="fragment">Support discovery and use of optimized datasets
<li class="fragment">Standardize interfaces for training and fine-tuning models
<li class="fragment">Highlight model and dataset interfaces and compatibility
</ul>

---

## Package types

<ul>
<li class="fragment">Source package
<li class="fragment">Trained model (e.g. saved model format)
<li class="fragment">Dataset (e.g. tfrecord format)
</ul>

---

### Examples

<table style="font-size:80%;white-space:nowrap">

<tr>
<th>name</th>
<th>type</th>
<th>description</th>
</tr>

<tr>
<td>cifar10</td>
<td>dataset</td>
<td>TF records for CIFAR-10 dataset</td>
</tr>

<tr>
<td>mnist</td>
<td>dataset</td>
<td>TF records for MNIST dataset</td>
</tr>

<tr>
<td>inception-v1+ilsvrc2012</td>
<td>model</td>
<td>Inception v1 trained with<br>ILSVRC-2012</td>
</tr>

<tr>
<td>inception-v3+ilsvrc2012</td>
<td>model</td>
<td>Inception v3 trained with<br>ILSVRC-2012</td>
</tr>

<tr>
<td>inception-v1-src</td>
<td>source</td>
<td>TFSlim Inception v1 source</td>
</tr>

<tr>
<td>mnist-tutorial-src</td>
<td>source</td>
<td>TensorFlow MNIST tutorial source</td>
</tr>

</table>

---

## Package operations

<ul>
<li class="fragment">package
<li class="fragment">publish
<li class="fragment">search
<li class="fragment">install
<li class="fragment">uninstall
<li class="fragment">upgrade
</ul>

---

## Using source packages

<ul>
<li class="fragment">init --template PACKAGE
<li class="fragment">train
<li class="fragment">evaluate
<li class="fragment">deploy
<li class="fragment">serve
</ul>

---

## Packaging work flow

<ul>
<li class="fragment">Identify candidate project
<li class="fragment">Name project
<li class="fragment">`GuildPkg` and `packager` files
<li class="fragment">Guild `package` to generate archive
<li class="fragment">Guild `publish` to publish archive to mirror
</ul>

---

## Best practices

<ul>
<li class="fragment">Minimize changes to upstream sources
<li class="fragment">Use patch files or wrap code as needed
<li class="fragment">Work with standard interfaces (FLAGS, summaries, saved models, etc.)
</ul>

---

<h4 style="text-transform:none"><code>mnist-tutorial-src/GuildPkg</code></h4>

<pre>
[package]

  name = mnist-tutorial-src
  version = 1
  source = \
      https://github.com/tensorflow/.../tutorials/mnist \
      mnist_deep_with_summaries.py \
      tensorflow.patch \
      Guild.in
  packager = packager

[references]

  github = https://github.com/tensorflow/.../tutorials/mnist
</pre>

---

<h4 style="text-transform:none"><code>mnist-tutorial-src/packager</code></h4>

<pre>
prepare() {
    cd "$srcdir/tensorflow"
    patch -p1 < ../tensorflow.patch
}

package() {
    cp "$srcdir/Guild.in" "$pkgdir"
    cp "$srcdir/"*.py "$pkgdir"
    cp "$srcdir/tensorflow/examples/tutorials/mnist/"*.py \
       "$pkgdir"
}
</pre>

---

<h4 style="text-transform:none"><code>tensorflow.patch</code></h4>

<pre>
@@ -149,7 +149,7 @@
   def feed_dict(train):
     """Make a TensorFlow feed_dict: maps data onto Tensor placeholders."""
     if train or FLAGS.fake_data:
-      xs, ys = mnist.train.next_batch(100, fake_data=FLAGS.fake_data)
+      xs, ys = mnist.train.next_batch(FLAGS.batch_size, fake_data=FLAGS.fake_data)
       k = FLAGS.dropout
     else:
       xs, ys = mnist.test.images, mnist.test.labels

...
</pre>

---

# Demo

---

## References

- https://guild.ai - Guild AI general
- https://github.com/guildai/guild - bleeding edge packaging support
- https://github.com/guildai/guild-packages - bleeding edge package defs
