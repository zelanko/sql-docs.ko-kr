---
title: AMO 보완 클래스 및 메서드 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- restores [AMO]
- assemblies [AMO]
- AMO, backup and restore
- capture logs [AMO]
- programming [AMO]
- Analysis Management Objects, backup and restore
- traces [AMO]
- backups [AMO]
ms.assetid: 14aed554-d2e2-49e5-9c72-26660759bce2
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 66fcd0c30acb2ddf62288cb549b96b74ebf7f7b9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37317333"
---
# <a name="programming-amo-complementary-classes-and-methods"></a>AMO 보완 클래스 및 메서드 프로그래밍
  이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [Assembly 클래스](#Assembly)  
  
-   [백업 및 복원](#BU)  
  
-   [Trace 클래스](#TRC)  
  
-   [Capturelog 및 CaptureXML 특성](#CL)  
  
##  <a name="Assembly"></a> Assembly 클래스  
 어셈블리의 기능을 확장 하는 사용자 수 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 새 저장된 프로시저 또는 MDX (Multidimensional Expressions) 함수를 추가 하 여 합니다. 자세한 내용은 [AMO 기타 클래스 및 메서드](amo-other-classes-and-methods.md)합니다.  
  
 어셈블리를 추가하거나 삭제하는 작업은 간단하며 온라인으로 수행할 수 있습니다. 단, 어셈블리를 데이터베이스에 추가하려면 데이터베이스 관리자여야 하며 서버 개체에 추가하려면 서버 관리자여야 합니다.  
  
 다음 예제에서는 지정된 데이터베이스에 어셈블리를 추가하고 어셈블리를 실행할 서비스 계정을 할당합니다. 같은 어셈블리가 데이터베이스에 있으면 새 어셈블리를 추가하기 전에 해당 어셈블리를 삭제합니다.  
  
```  
static public void CreateStoredProcedures(Database db)  
{  
    ClrAssembly clrAssembly;  
  
    // Verify That assembly exist in database and drop it  
    if (db.Assemblies.ContainsName("StoredProcedures"))  
    {  
        clrAssembly = db.Assemblies.FindByName("StoredProcedures");  
        clrAssembly.Drop();  
    }  
  
    // Create the CLR assembly  
    clrAssembly = db.Assemblies.Add("StoredProcedures");  
    clrAssembly.ImpersonationInfo = new ImpersonationInfo(  
        ImpersonationMode.ImpersonateServiceAccount);  
    clrAssembly.PermissionSet = PermissionSet.Unrestricted;  
  
    // Load the assembly files  
    clrAssembly.LoadFiles(Environment.CurrentDirectory  
        + @"\StoredProcedures2.dll", false);  
  
    clrAssembly.Update();  
}  
  
```  
  
##  <a name="BU"></a> Backup 및 Restore 메서드  
 관리자는 Backup 및 Restore 메서드를 사용하여 데이터베이스를 백업하고 복원할 수 있습니다.  
  
 다음 예제에서는 지정된 서버에 있는 모든 데이터베이스의 백업본을 만듭니다. 백업 파일이 이미 있으면 해당 파일을 덮어씁니다. 백업 파일은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Data 폴더의 BackUp 폴더에 저장됩니다.  
  
```  
static public void BackUpAllDatabases(Server svr)  
{  
    string fileName;  
    if ((svr != null) && ( svr.Connected))  
        foreach (Database db in svr.Databases)  
        {  
            fileName = db.Name + "_" + ((Int64)(DateTime.Today.Year * 10000 + DateTime.Today.Month * 100 + DateTime.Today.Day)).ToString()+ ".abf";  
            db.Backup(fileName, true);  
        }  
}  
```  
  
 다음 예제에서는 앞의 예제에서 만든 "Adventure Works" 백업본을 복원합니다. "My Adventure WorksDW" 데이터베이스가 이미 있으면 해당 데이터베이스를 덮어씁니다.  
  
```  
static public void RestoreAdventureWorks(Server svr)  
{  
    svr.Restore("Adventure Works DW_20051025.abf", "My Adventure WorksDW", true);  
}  
```  
  
##  <a name="TRC"></a> Trace 클래스  
 서버 작업을 모니터링하려면 세션 추적과 서버 추적이라는 두 종류의 추적 기능을 사용해야 합니다. 서버를 추적하면 서버에서 현재 태스크가 수행되고 있는 방식을 확인하거나(세션 추적) 서버에 연결하지 않고도 서버의 전체 작업에 대한 정보를 확인할 수 있습니다(서버 추적).  
  
 세션 추적을 통해 현재 작업을 추적할 때 서버에서는 해당 서버에서 발생하는 이벤트 중 응용 프로그램으로 인해 발생한 이벤트에 대한 알림을 현재 응용 프로그램에 보냅니다. 이벤트는 현재 응용 프로그램의 이벤트 처리기를 사용하여 캡처됩니다. 먼저 <xref:Microsoft.AnalysisServices.SessionTrace> 개체에 이벤트 처리 루틴을 할당한 다음 세션 추적을 시작합니다.  
  
 다음 예제에서는 세션 추적을 설정하여 현재 작업을 추적하는 방법을 보여 줍니다. 예제의 맨 끝에 있는 이벤트 처리기 루틴은 모든 추적 정보를 System.Console 개체에 출력합니다. 추적이 시작된 후에는 추적 이벤트를 생성하기 위해 "Adventure Works" 예제 큐브가 완전히 처리됩니다.  
  
```  
static public void TestSessionTraces(Server svr)  
{  
    // Start the default trace  
  
    svr.SessionTrace.OnEvent  
        += new TraceEventHandler(DefaultTrace_OnEvent);  
    svr.SessionTrace.Stopped  
        += new TraceStoppedEventHandler(DefaultTrace_Stopped);  
    svr.SessionTrace.Start();  
  
    // Process the databases  
    // The trace handlers will output all progress notifications   
    // to the console  
    Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    cube.Process(ProcessType.ProcessFull);  
  
    // Stop the default trace  
    svr.SessionTrace.Stop();  
  
}  
static public void DefaultTrace_OnEvent(object sender, TraceEventArgs e)  
{  
    Console.WriteLine("{0}", e.TextData);  
}  
  
static public void DefaultTrace_Stopped(ITrace sender, TraceStoppedEventArgs e)  
{  
    switch (e.StopCause)  
    {  
        case TraceStopCause.StoppedByUser:  
        case TraceStopCause.Finished:  
            Console.WriteLine("Processing completed successfully");  
            break;  
  
        case TraceStopCause.StoppedByException:  
            Console.WriteLine("Processing failed: {0}",  
                e.Exception.Message);  
            break;  
    }  
}  
```  
  
 서버 추적에서는 모든 사항을 추적 파일에 기록하도록 구성할 수 있으며 서비스가 다시 시작될 때 서버 추적도 자동으로 다시 시작할 수 있습니다.  
  
 서버 추적을 설정하려면 먼저 서버에서 모니터링할 이벤트와 추적 파일에 저장할 이벤트 데이터를 정의해야 합니다. 각 이벤트에 추적 파일에 저장할 데이터 열을 정의해야 합니다.  
  
 서버 추적을 만들려면 다음 네 단계를 수행해야 합니다.  
  
1.  서버 추적 개체를 만들고 기본 공통 특성을 채웁니다.  
  
     LogFileSize는 추적 파일의 최대 크기를 정의하며 메가바이트 단위로 정의됩니다. LogFileRollOver를 사용하면 LogFileSize 제한이 초과될 때 다른 파일에서 로그 파일이 시작될 수 있으며 이때 파일 이름에는 시퀀스 번호가 추가됩니다. AutoRestart를 사용하면 서비스가 다시 시작될 경우 추적이 다시 시작됩니다.  
  
2.  이벤트와 해당 데이터 열을 만듭니다.  
  
3.  필요한 경우 추적을 시작하고 중지합니다.  
  
     추적이 중지된 후에도 해당 추적은 서버에 존재하며 추적이 AutoRestart=`true`로 정의된 경우에는 다시 시작됩니다.  
  
4.  추적이 더 이상 필요하지 않으면 추적을 삭제합니다.  
  
 다음 예제에서는 추적이 이미 파티션이 있을 경우 삭제된 후 다시 만들어집니다. 추적 파일은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 폴더의 Log 폴더에 저장됩니다.  
  
```  
static public void TestServerTraces(Server svr)  
{  
    Trace trc;  
    TraceEvent te;  
  
        trc = svr.Traces.FindByName("TestServerTraces");  
        if (trc != null)  
            trc.Drop();  
        trc = svr.Traces.Add("TestServerTraces", "TestServerTraces");  
        trc.LogFileName = ("TestServerTraces_" +((Int64)(DateTime.Now.Year * 10000 + DateTime.Now.Month * 100 + DateTime.Now.Day)).ToString() + "_" +  
                ((Int64)(DateTime.Now.Hour * 10000 + DateTime.Now.Minute * 100 + DateTime.Now.Second)).ToString() + ".trc");  
        trc.LogFileSize = 100;  
        trc.LogFileRollover = true;  
        trc.AutoRestart = false;  
  
        #region Define Events to trace & data columns per event  
        te = trc.Events.Add(TraceEventClass.ProgressReportBegin);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportCurrent);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportEnd);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.EndTime);  
        te.Columns.Add(TraceColumn.Success);  
        te.Columns.Add(TraceColumn.Error);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
        #endregion  
  
        trc.Update();  
        trc.Start();  
  
        #region Process the Adventure Works Cube  
        // The trace settings will output all progress notifications   
        // to the trace file  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        Cube cube = db.Cubes.FindByName("Adventure Works");  
        cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        trc.Stop();  
        trc.Drop();  
  
}  
```  
  
##  <a name="CL"></a> CaptureLog 및 CaptureXml 특성  
 CaptureLog 특성을 사용하면 AMO 작업에서 XMLA 배치 파일을 만들 수 있습니다. 또한 서버 개체를 데이터베이스, 큐브, 차원, 마이닝 구조 등으로 스크립팅할 수 있습니다.  
  
 CaptureLog를 만들려면 다음 단계를 수행해야 합니다.  
  
1.  서버 특성 CaptureXml을 `true`로 설정하여 XMLA 로그를 캡처하기 시작합니다.  
  
     이 옵션을 설정하면 모든 AMO 작업이 서버로 보내지는 대신 문자열 컬렉션에 저장되기 시작합니다.  
  
2.  일반적인 방법대로 AMO 작업을 시작합니다. 하지만 이때 아무 동작도 서버로 보내지지 않습니다. AMO 작업은 처리, 만들기, 삭제, 업데이트 또는 개체에 대한 기타 동작과 같은 작업일 수 있습니다.  
  
3.  CaptureXml을 `false`로 설정하여 XMLA 로그 캡처를 중지합니다.  
  
4.  CaptureLog 문자열 컬렉션의 각 문자열을 검토하거나 ConcatenateCaptureLog 메서드로 완전한 문자열을 생성하여 캡처된 XMLA를 검토합니다. ConcatenateCaptureLog를 사용하면 XMLA 일괄 처리를 단일 트랜잭션으로 생성하고 이 일괄 처리에 병렬 처리 옵션을 추가할 수 있습니다.  
  
 다음 예제에서는 [Adventure Works DW Multidimensional 2012] 데이터베이스의 모든 차원과 모든 큐브에 대해 전체 처리를 수행하는 일괄 처리 명령이 들어 있는 문자열을 반환합니다.  
  
```  
static public string TestCaptureLog(Server svr)  
{  
    String capturedXmla = "";  
    if ((svr != null) && (svr.Connected))  
    {  
        svr.CaptureXml = true;  
  
        #region Actions to be captured to an XMLA file  
        //No action is executed during CaptureXml = true  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        foreach (Dimension dim in db.Dimensions)  
            dim.Process(ProcessType.ProcessFull);  
        foreach (Cube cube in db.Cubes)  
            cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        svr.CaptureXml = false;  
  
        capturedXmla = svr.ConcatenateCaptureLog(true, true);  
  
    }  
  
    return capturedXmla;  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices>   
 [AMO 클래스 소개](amo-classes-introduction.md)   
 [AMO 기타 클래스 및 메서드](amo-other-classes-and-methods.md)   
 [논리적 아키텍처 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [다차원 모델 개체 처리](../processing-a-multidimensional-model-analysis-services.md)  
  
  
