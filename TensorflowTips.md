# Tensorflow Tips

Here is some tips for tensorflow1.x.

1.   print tensor

     ```python
     self.p = tf.Print(<input tensor>, ['<message>', <printed tensor>], summarize=100)
     
     sess.run(model.p)
     ```

2.   print model weight. find the corresponding op name in tensorboard

     ```python
     weight=tf.get_default_graph().get_tensor_by_name("<operation name>:0")
     
     print(sess.run(weight))
     ```

3.   print model weight. find the corresponding op name in tensorboard

     ```python
     weight=tf.get_default_graph().get_tensor_by_name("<operation name>:0")
     
     print(sess.run(weight))
     ```

