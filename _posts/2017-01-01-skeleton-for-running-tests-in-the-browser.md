---
layout: post
title:  "A skeleton for running tests in the browser"
date:   2017-01-01 09:02:01 +0000
categories: blog
author: dumitru panaghiea
---
While writing Javascript code I felt the need to have a playground project where I can run snippets of code without having to execute shell commands all the time. I have created a simple project that helped me with this.

It consists of an `index.html` and a `specs.js` file that contains the tests.
When the [server][live-server] is running it will look for any changes in the tests and reload the browser.

{% highlight HTML %}

<html>
<head>
  <meta charset="utf-8">
  <title>Mocha Tests</title>
  <link href="node_modules/mocha/mocha.css" rel="stylesheet" />
</head>
<body>
  <div id="mocha"></div>

  <script src="node_modules/jquery/dist/jquery.min.js"></script>
  <script src="node_modules/chai/chai.js"></script>
  <script src="node_modules/mocha/mocha.js"></script>

  <script>mocha.setup('bdd')</script>
  <script src="specs.js"></script>

<script>
    mocha.checkLeaks();
    mocha.globals(['jQuery']);
    mocha.run();
  </script>
</body>
</html>
{% endhighlight %}

{% highlight JavaScript %}
var should = chai.should;
chai.should();

describe('Example of tests that run automatically when specs.js is modified', () => {
    describe('This suite will demonstrate the way mocha displays passing and failing tests', () => {
        it('This test should pass', () => {
            let str = "1";
            str.should.be.a('string');
        });
        it('This test should faill', () => {
            let int = "0";
            int.should.be.a('number');
        });
    });
});
{% endhighlight %}

Check out the [repo link][repo-link] for instructions on how to run it.

[repo-link]: https://github.com/panagdu/browser-tests-skeleton
[live-server]: https://github.com/tapio/live-server