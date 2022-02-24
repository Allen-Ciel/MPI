# MPI
Visual Studio2019配置MPI环境

mpi官方下载地址：http://www.mpich.org/downloads/

Windows10+Visual Studio2019

1.文件-新建-项目

2.空项目

3.项目-添加新项

4.C++文件（.cpp）

5.右击项目-->>属性，进行配置： 

6.右上角-->>配置管理器-->>活动解决方案平台，选择：x64

7.VC++目录-->>包含目录，添加：“D:\Program Files (x86)\Microsoft SDKs\MPI\Include;” 

8.VC++目录-->>库目录，添加：“D:\Program Files (x86)\Microsoft SDKs\MPI\Lib\x64;”  

9.C/C++ -->> 预处理器-->>预处理器定义，添加：“MPICH_SKIP_MPICXX;” 

10.C/C++ -->> 代码生成 -->> 运行库，选择：多线程调试（/MTd）

11.链接器 -->> 输入 -->> 附加依赖项，添加：“msmpi.lib;”


12.测试代码
#include<stdio.h>
#include "mpi.h"
int main(int argc, char* argv[]) {
    int numtasks, rank, rc;
    rc = MPI_Init(&argc, &argv);
    if (rc != MPI_SUCCESS) {
        printf("Error starting MPI program. Terminating.\n");
        MPI_Abort(MPI_COMM_WORLD, rc);
    }
    MPI_Comm_size(MPI_COMM_WORLD, &numtasks);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    printf("Number of tasks= %d My rank= %d\n", numtasks, rank);
    MPI_Finalize();


13.运行

编译后在命令行打开

命令：mpiexec -n 10 MPI_test.exe #-n 10 表示开十个线程
