.. _cn_api_fluid_layers_uniform_random_batch_size_like:

uniform_random_batch_size_like
-------------------------------

.. py:function:: paddle.fluid.layers.uniform_random_batch_size_like(input, shape, dtype='float32', input_dim_idx=0, output_dim_idx=0, min=-1.0, max=1.0, seed=0)

该OP使用从范围[min，max)内均匀分布采样的随机值初始化一个Tensor，且输出Tensor的
指定维度将被设置为与输入Tensor指定维度相同的值。

::

    示例1:
              给定：  
                   input =[[0.946741  , 0.1357001 , 0.38086128]]    # input.shape=[1,3]
                   shape=[2,4]
              此时，output_dim_idx = 0， input_dim_idx = 0，result.shape[0] = input.shape[0]
              则：
                   result=[[ 0.3443427 , -0.23056602,  0.3477049 ,  0.06139076]]    # result.shape=[1,4]

    示例2:
              给定：
                   input =[[0.946741  , 0.1357001 , 0.38086128]]     # input.shape=[1,3]
                   shape=[2,4]
                   input_dim_idx=1
                   output_dim_idx=1
              此时，output_dim_idx = 1， input_dim_idx = 1，result.shape[1] = input.shape[1]
              则：
                   result=[[-0.23133647, -0.84195036,  0.21441269],
                          [-0.08774924,  0.25605237, -0.09403259]]    # result.shape=[2,3]

参数：
        - **input** （Variable）- 输入Tensor，支持的数据类型：float32。
        - **shape** （list|tuple）- 输出Tensor的维度，类型为list或者tuple。支持的数据类型：int。
        - **input_dim_idx** （int，可选）- 输入Tensor指定维度的索引。该参数指定输入Tensor维度的值将用于调整输出Tensor维度的大小。支持的数据类型：int。默认值为0。
        - **output_dim_idx** （int，可选）- 输出Tensor指定维度的索引。该参数指定输出Tensor的维度将被设置为与输入Tensor指定维度相同的值。支持的数据类型：int。默认值为0。
        - **min** （float，可选）- 要生成的随机值范围的下限，min包含在范围中。支持的数据类型：float。默认值为 1.0。
        - **max** （float，可选）- 要生成的随机值范围的上限，max不包含在范围中。支持的数据类型：float。默认值为1.0。
        - **seed** （int，可选）- 用于生成样本的随机种子。0表示使用系统生成的种子，数据类型为int。注意如果seed不为0，则此算子将始终每次生成相同的随机数。支持的数据类型：int。默认值为0。
        - **dtype** （np.dtype | core.VarDesc.VarType | str，可选） - 输出Tensor的数据类型。支持的数据类型：float32， float64，默认值为float32。

返回:      表示随机初始化结果的Tensor，数据类型由dtype参数设置，该Tensor的维度由shape参数和输入Tensor的指定维度共同决定。

返回类型:        Variable


**代码示例：**

.. code-block:: python

    import paddle.fluid as fluid
    import paddle.fluid.layers as layers
    
    
    input = fluid.data(name="input", shape=[13, 11], dtype='float32')
    # examp 1:
    # input_dim_idx和output_dim_idx使用默认值 
    out1 = layers.uniform_random_batch_size_like(input, [3, 5]) 
    out1_shape = layers.shape(out1) # [13,5]
   
    # example 2:
    # input_dim_idx和output_dim_idx使用指定值
    out2=layers.uniform_random_batch_size_like(input, [3, 5], input_dim_idx=1, output_dim_idx=1)
    out2_shape = layers.shape(out2) # [3,11]        




