---
title: 关于Yii的beforeAction，afterAction的用法
author: gxbsst
layout: post
permalink: /archives/255
post_views_count:
  - 201
views:
  - 149
categories:
  - PHP
---
有一个业务逻辑是这样: 如果订单已经成功，我则需要清空购物车，如果购物车为空，那么则不能执行几个Actions，如: checkout, confirm等, 我想框架应该都有beforeAction，一查API，真的可以找到，也看到YII的框架的CController源代码有这么一段:

<pre lang="php">* Runs the action after passing through all filters.
   * This method is invoked by {@link runActionWithFilters} after all possible filters have been executed
   * and the action starts to run.
   * @param CAction action to run
   */
  public function runAction($action)
  {
    $priorAction=$this->_action;
    $this->_action=$action;
    if($this->beforeAction($action))
    {
      $action->run();
      $this->afterAction($action);
    }
    $this->_action=$priorAction;
  }
</pre>

从这里可以看出，YII在每执行一个阿城题噢你都要经过beforeAction，$action, afterAction, 那么我可以Overwrite这两个方法达到我想要的效果:

<pre lang="php">#如果购物成功，则要清空购物车的东西.
  protected  function afterAction( $action ){
    if ($action->getId() == 'success') {
      Yii::app()->session->remove('cart');
      Yii::app()->session->remove('order');
    }
  }

  #如购物车没有东西，则不能执行除buy以外的操作
  protected  function beforeAction( $action ){
    $action = $action->getId();
    if ( $action != 'buy') {
      $this->redirect(Yii::app()->homeUrl);
    }
  }

</pre>

* 从这里看出，有点filter的意思!

&#8211;EOF&#8211;

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于Yii的beforeAction，afterAction的用法][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/255