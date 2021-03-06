# Genealogy-Management-System
# Update
## ver 5.0 2020/1/1
1. 修复了根节点为空时访问空指针错误的问题 `详细:914行增加 if(p == NULL) break; // 根节点为空`
## 2019/12/27
1. 1068 1072行性别不对 应该追究到apple函数中, apple函数中关系相反了
## ver 4.0 2019/12/26
1. 确定俩人之间的关系
2. 修复了一些小bug
## ver 3.0 2019/12/24
1. 代码功能完善暂未发现bug
2. 支持不同关系的录入和按条件输出
3. 条件输出应根据输入的姓名和前几代或后几代来输出
4. tagert: 输入两人的姓名可以输出两人的关系
## 2019/12/23
1. 用fileOpenFlag == TRUE代替mychbrotree != NULL来判断文件是否打开
2. 增加文件未打开时close的提示语
3. 增加了内存释放机制 delAllTree() 放弃使用时清空整个树的内存
## 2019/12/22 
1. 160行treeInput无法输入到myinfo结构体中的bug无法复现
2. save中的fwrite无法写入已修复::由于output为分配文件指针
3. 重构case 3: open, 优化代码
4. 文件基本操作 输入 输出 新建 读取 关闭 保存部分的已知bug已排除
## ver 2.0 2019/12/21
1. 更新并完善的数据文件处理机制 详细：可以新建，查看，关闭数据文件
2. 树型数据结构基本完成
3. 遗留bug：160行treeInput无法输入到myinfo结构体中 305行：save中的fwrite无法写入
4. case 5后的代码还未进行检验
## ver 1.0 2019/12/16

# 任务分配
1. 组长： 项目整体框架，涉及文件操作，数据声明，数据输出格式
2. 组员： 对数据结构的操作，插入删除修改结点, 查找，其他的亲属关系，按条件输出
# mession 
1. 待议索引: 对超过1的姓名建立索引，先查找索引是否存在，存在遍历整个表
# 需求分析
1. 将关系族谱转换为树，并使用树的孩子兄弟表示法
2. 输入时先保存到内存，然后从内存转存到硬盘
3. 从硬盘读取数据到内存
# 对于族谱：
在一个家族族谱中，是以男性为主导的族谱，所以女方的丈夫是没有权利进入家谱的。这里就可以排除与女方丈夫的关系，即：没有丈母娘和老丈人的关系及与女方娘家的所有关系都排除在外接着就是在数据的存储方面，我们在保存男方的妻子时，其妻子的父亲和母亲是为空的，她只是记录了丈夫的Id，所以在判断她和别人的关系就要先找到她的丈夫，然后以她丈夫的身份去判断。
然后讲的就是算法的实现：

1. 先判断在族谱中是否存在这两人。这里也会判断当名字一样的情况。
2. 从数据库中取出这两人的数据
3. 如果是某人的妻子就拿到她的丈夫在树中的节点。（区分女儿和男方妻子）
4. 判断两人数据中的代系，即区分同代和不同代的，以此再分开来判断两人关系
5. 根据区分开来的代系，判断同代的关系。在同代中有亲，堂，表的三个关系链，当然还有夫妻这一层关系。
6. 当是异代的时候，在这里又要区分是差几代的情况，根据实际的情况，判断的都是三代和三代以内的关系，即到了爷爷辈之后就不提供关系的判断了。异代的关系判断走的是直系和旁系这两条线，因为在一个家族中当人口达到一定的数量时，就会产生直系和旁系的明显区别，所以在做判断的，添加了直旁系的判断以此来增强程序的健壮性和可持续性。

# sparkle
1. 2019/12/16 Liukai 增加校验程序，对于大量测试代码，应生成从零开始的长度固定的16进制数，输出树后，将期望生成的树和目标生成的树进行校验
2. 2019/12/16 Liukai 程序应可以生成不只有一个族谱的族谱图（采用文件管理）
3. 2019/12/24 LiuXiaoxia 族谱的录入->树 查重
5. 查找  族谱的输出 向上或向下多少代
6. 父系，母系
7. 发现同一祖先的时候合并 
8. // void del();
9. 必须指明是谁的后代
---
## 项目说明
题目五：家族关系查询系统

1.【问题描述】

建立家族关系数据库，实现对家族成员关系的相关查询。

2.【基本要求】

建立家族关系并存储到文件中；实现家族成员的添加；查询家族成员的双亲、祖先、兄弟、孩子及后代信息。

说明:

1. 14周随堂给学生布置任务，17周周一找指导教师说明需求分析，并汇报任务分配情况，17周周一开始上机
2. 上机时间：上午：8：30-11：30	下午：14：00-17：30
3. 上机地点：主楼五层500（1,2,3,4班）、513（1,2,3,4班）房间
4. 上机要求：一组两台机器，允许带笔记本，每次（上午或下午）一位同学上机并签到（至少7-10次）
5. 需求分析：主要分析课题的内容、需要用的数据结构、小组分工情况；格式不限。（不用交给老师）
6. 课程设计说明书：一组一份。按规定格式书写，组长负责总体，每人完成各自部分。
7. 验收：软件功能包括任务书中的所有任务，每位同学讲解自己的部分；并向指导老师提交纸质课程设计说明书。
教师联系方式：13994233961
题目负责教师：张建华


