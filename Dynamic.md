<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">1，dynamic和var</span></p>
<p>①var声明局部变量只是一种简化语法，它要求编译器更具表达式推断具体数据类型</p>
<p>②var关键字只能在方法内部声明局部变量，而dynamic关键字可用于局部变量、字段和草书</p>
<p>③表达式不能转型为var，但能转型为dynamic</p>
<p>④必须显式初始化用var声明的变量，而无需初始化用dynamic声明的变量</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">2，dynamic和object</span></p>
<p>①dynamic表达式其实和object一样的类型</p>
<p>②针对dynamic无法智能感知</p>
<p>③可以对object扩展但不能对dynamic扩</p>