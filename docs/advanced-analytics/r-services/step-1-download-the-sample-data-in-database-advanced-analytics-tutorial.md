---
title: "1단계: 샘플 데이터 다운로드(데이터베이스 내 고급 분석 자습서) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 1단계: 샘플 데이터 다운로드(데이터베이스 내 고급 분석 자습서)
이 단계에서는 이 연습에 사용되는 샘플 데이터 집합 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일을 다운로드합니다. 데이터와 스크립트 파일 둘 다 Github에서 공유되지만 PowerShell 스크립트는 데이터 및 스크립트 파일을 선택한 로컬 디렉터리에 다운로드합니다.  
  
## 데이터 및 스크립트 다운로드  
  
1.  Windows PowerShell 명령 콘솔을 엽니다.  
  
    대상 디렉터리를 만들거나 지정된 대상에 파일을 쓰려면 관리자 권한이 필요한 경우 **관리자 권한으로 실행** 옵션을 사용합니다.  
  
2.  *DestDir* 매개 변수 값을 로컬 디렉터리로 변경하여 다음 PowerShell 명령을 실행합니다.  여기서 사용한 기본값은 **TempRSQL**입니다.  
  
    ```  
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’  
  
    ```  
  
    *DestDir*에 지정한 폴더가 존재하지 않을 경우 PowerShell 스크립트를 통해 생성됩니다.  
  
    > [!TIP]  
    > 오류가 발생할 경우 Bypass 인수를 사용하고 변경 범위를 현재 세션으로 지정하여 이 연습에 대해서만 PowerShell 스크립트 실행 정책을 일시적으로 **무제한**으로 설정할 수 있습니다.  
    >   
    >````  
    > Set\-ExecutionPolicy Bypass \-Scope Process  
    >````   
    > 이 명령을 실행해도 구성이 변경되지는 않습니다.  
  
    인터넷 연결에 따라 다운로드하는 데 시간이 걸릴 수도 있습니다.  
  
3.  모든 파일이 다운로드되면 PowerShell 스크립트가 *DestDir*에 지정된 폴더에서 열립니다. PowerShell 명령 프롬프트에서 다음 명령을 실행하고 다운로드된 파일을 검토합니다.  
  
    ```  
    ls  
    ```  
  
    **결과:**  
  
    ![list of files downloaded by PowerShell script](../../advanced-analytics/r-services/media/rsql-devtut-filelist.PNG "list of files downloaded by PowerShell script")  
  
## 다음 단계  
[2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## 이전 단계  
[SQL 개발자를 위한 데이터베이스 내 고급 분석&#40;자습서&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
## 참고 항목  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
