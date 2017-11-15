---
title: 利用python处理excel
date: 2016-11-23 14:19:24
tags: 自动处理
categories: 立信审计日记
---
2016年10月下旬到十一月上旬，我参与了云南变压器电气股份有限公司的审计项目。在处理往来款项的时候，云变公司的往来账款的发生额明细与去年底稿的审定明细有差异，有的公司有发生额没有余额，有的公司有余额没有往来发生额，因此在填写明细表时需要反复核对。在这种背景下，我产生了写一个自动脚本的想法。就这样，excel自动处理程序v1.0诞生了。利用python操作excel需要用
到两个模块，分别是xlwt进行写入和xlrd进行读取。下面是v1.0的部分代码。
<!-- more -->

    # -*- coding: utf-8 -*-
    import xlwt
    import xlrd
    from xlutils.copy import copy
    wb = xlrd.open_workbook("E:\\123.xls")
    worksheet = wb.sheets()[0]
        cols1 = worksheet.col_values(0)
    while "" in cols1:
        cols1.remove("")
    # print ("这是列表一")
    # print (cols)
    cols2 = worksheet.col_values(4)
    while "" in cols2:
        cols2.remove("")
    # print ("这是列表二")
    # print (cols2)
    SameList = []
    DfrList1 = []
    DfrList2 = []
    for each in cols1:
        if each in cols2:
            SameList.append(each)
        else :
            DfrList1.append(each)
    for each in cols2:
        if each in cols1:
            pass
        else:
            DfrList2.append(each)
    InitValue = []
    InitValue2 = []
    AddValue = []
    DelValue = []
    AddValue2 = []
    DelValue2 = []
    # print (SameList)
    # print (DfrList1)
    # print (DfrList2)
    x = 0
    while x<483:
        a = worksheet.cell(x,1).value
        if worksheet.cell(x,0).value in SameList:
            AddValue.append(a)
            x+=1
        elif worksheet.cell(x,0).value in DfrList1 :
            AddValue2.append(a)
            x+=1
        else:
            x+=1
    # print (AddValue)
    # print (AddValue2)
    x = 0
    while x<483:
    d = worksheet.cell(x,2).value
    if worksheet.cell(x,0).value in SameList:
        DelValue.append(d)
        x+=1
    elif worksheet.cell(x,0).value in DfrList1:
        DelValue2.append(d)
        x+=1
    else:
        x+=1
    # print (DelValue)
    # print(DelValue2)

    y = 0
    while y<346:
        i = worksheet.cell(y,5).value
        if worksheet.cell(y,4).value in SameList:
            InitValue.append(i)
            y+=1
        elif worksheet.cell(y,4).value in DfrList2:
            InitValue2.append(i)
            y+=1
        else :
            y+=1
    # print (InitValue)
    # print (InitValue2)

其中核心逻辑部分循环代码跟杨晨昊交流了意见，采用了while和for in的循环结构。程序基本完成。但是此时需要新建工作表来进行写入，并且需要将表格放在指定位置并指定命名，在测试员孙开使用后效果并不理想。因此我决定采用easygui模块进行图像界面交互，能够选择文件位置再行处理；同时还采用了xlutils模块，能够在原来读取的工作表中进行写入操作。最终在反复修改后诞生了现在的excel自动处理程序v2.1.下面是程序的全部代码。

    # -*- coding: utf-8 -*-
    import xlwt
    import xlrd
    import easygui as g
    from xlutils.copy import copy
    choice=[]
    choice.append("朕知道了")
    g.buttonbox(msg="请务必保持原文件已处理成以下格式",image = "excel.gif",choices=choice,title="警告：如果格式错误将处理失败")
    doc=g.fileopenbox()
    doc=doc[0:2]+"\\\\"+doc[3:]
    wb = xlrd.open_workbook(doc)
    worksheet = wb.sheets()[0]
    cols1 = worksheet.col_values(0)
    while "" in cols1:
        cols1.remove("")
    # print ("这是列表一")
    # print (cols)
    cols2 = worksheet.col_values(4)
    while "" in cols2:
        cols2.remove("")
    # print ("这是列表二")
    # print (cols2)
    SameList = []
    DfrList1 = []
    DfrList2 = []
    for each in cols1:
        if each in cols2:
            SameList.append(each)
        else :
            DfrList1.append(each)
    for each in cols2:
        if each in cols1:
            pass
        else:
            DfrList2.append(each)
    InitValue = []
    InitValue2 = []
    AddValue = []
    DelValue = []
    AddValue2 = []
    DelValue2 = []
    # print (SameList)
    # print (DfrList1)
    # print (DfrList2)
    x = 0
    while x<len(cols1):
        a = worksheet.cell(x,1).value
        if worksheet.cell(x,0).value in SameList:
            AddValue.append(a)
            x+=1
        elif worksheet.cell(x,0).value in DfrList1 :
            AddValue2.append(a)
            x+=1
        else:
            x+=1
    # print (AddValue)
    # print (AddValue2)
    x = 0
    while x<len(cols1):
        d = worksheet.cell(x,2).value
        if worksheet.cell(x,0).value in SameList:
            DelValue.append(d)
            x+=1
        elif worksheet.cell(x,0).value in DfrList1:
            DelValue2.append(d)
            x+=1
        else:
            x+=1
    # print (DelValue)
    # print(DelValue2)

    y = 0
    while y<len(cols2):
        i = worksheet.cell(y,5).value
        if worksheet.cell(y,4).value in SameList:
            InitValue.append(i)
            y+=1
        elif worksheet.cell(y,4).value in DfrList2:
            InitValue2.append(i)
            y+=1
        else :
            y+=1
    # print (InitValue)
    # print (InitValue2)
    # 开始进行写入
    oldwb = xlrd.open_workbook(doc)
    Newwb = copy(oldwb)
    Newws = Newwb.get_sheet(0)
    # 有期初有发生额
    for n in range(len(SameList)):    
        Newws.write(n,7,SameList[n])
    for i in range(len(InitValue)):
        Newws.write(i,8,InitValue[i])
    for a in range(len(AddValue)):
        Newws.write(a,9,AddValue[a])
    for d in range(len(DelValue)):
        Newws.write(d,10,DelValue[d])
    # 无期初有发生额
    StyleRed = xlwt.easyxf("pattern:pattern solid,fore_colour red;font:bold on;")
    for z in range(len(DfrList1)):
        Newws.write(len(SameList)+z,7,DfrList1[z],StyleRed)
    for x in range(len(DfrList1)):
        Newws.write(len(SameList)+x,8,0,StyleRed)
    for c in range(len(AddValue2)):
        Newws.write(len(SameList)+c,9,AddValue2[c],StyleRed)
    for v in range(len(DelValue2)):
        Newws.write(len(SameList)+v,10,DelValue2[v],StyleRed)
    # 有期初无发生额
    StyleBlue = xlwt.easyxf("pattern:pattern solid,fore_colour light_blue;font:bold on;")
    for z in range(len(DfrList2)):
        Newws.write(len(SameList)+len(DfrList1)+z,7,DfrList2[z],StyleBlue)
    for x in range(len(InitValue2)):
        Newws.write(len(SameList)+len(DfrList1)+x,8,InitValue2[x],StyleBlue)
    for c in range(len(InitValue2)):
        Newws.write(len(SameList)+len(DfrList1)+c,9,0,StyleBlue)
    for v in range(len(InitValue2)):
        Newws.write(len(SameList)+len(DfrList1)+v,10,0,StyleBlue)
    Newwb.save(doc)
    g.msgbox(msg="处理成功!如果excel无法打开请将后缀改成xls文件",title = "请稍后",ok_button = "O(∩_∩)O谢谢!")
