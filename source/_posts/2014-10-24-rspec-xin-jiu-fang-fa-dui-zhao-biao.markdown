---
layout: post
title: "Rspec 新旧方法对照表"
date: 2014-10-24 10:33:47 +0800
comments: true
categories: Rails Rspec
---

``` ruby
obj.should ...
expect(obj).to ...
```
``` ruby
obj.should_not ...
expect(obj).not_to ...
```
``` ruby
obj.should =~ //
expect(obj).to match(//)
```
``` ruby
[1, 2, 3].should =~ [3, 2, 1]
expect([1, 2, 3]).to match_array([3, 2, 1])
```
``` ruby
obj.should > 3
expect(obj).to be > 3
```
``` ruby
lambda { ... }.should raise_error
expect { ... }.to raise_error
```

## RSpec 2.14.0 or later

``` ruby
obj.stub(:foo)
allow(obj).to receive(:foo)
```
``` ruby
SomeClass.any_instance.should_receive(:foo)
expect_any_instance_of(SomeClass).to receive(:foo)
```
``` ruby
SomeClass.any_instance.stub(:foo)
allow_any_instance_of(SomeClass).to receive(:foo)
```

## RSpec 2.99.0.beta1 or later

``` ruby
it { should eq(something) }
it { is_expected.to eq(something) }
```

## RSpec 3.0.0.beta1 or later

``` ruby
obj.stub_chain(:foo, :bar).and_return(something)
allow(obj).to receive_message_chain(:foo, :bar).and_return(something)
```
