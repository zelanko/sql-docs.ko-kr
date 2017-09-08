---
title: "1 단계: 예제 데이터 다운로드 | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 147860e9af8cce86d1a7ccbd3e53f20d240fcd49
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="step-1-download-the-sample-data"></a>1단계: 샘플 데이터 다운로드

이 단계에서는 샘플 데이터 집합 및 스크립트를 다운로드할 수 있습니다. 데이터와 스크립트 파일 둘 다 Github에서 공유되지만 PowerShell 스크립트는 데이터 및 스크립트 파일을 선택한 로컬 디렉터리에 다운로드합니다.

## <a name="download-the-data-and-scripts"></a>데이터 및 스크립트 다운로드

1. Windows PowerShell 명령 콘솔을 엽니다.

    옵션을 사용 하 여 **관리자 권한으로 실행**, 대상 디렉터리를 만들거나 지정된 된 대상에 파일 기록 관리 권한이 필요 합니다.

2. *DestDir* 매개 변수 값을 로컬 디렉터리로 변경하여 다음 PowerShell 명령을 실행합니다.  여기 사용한 기본값인 **TempPythonSQL**합니다.

    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\tempPythonSQL'
    ```
    
    *DestDir* 에 지정한 폴더가 존재하지 않을 경우 PowerShell 스크립트를 통해 생성됩니다.
    
    오류가 발생 하는 경우에 PowerShell 스크립트의 실행 정책을 일시적으로 설정할 수 있습니다 **무제한** 를 사용 하 여이 연습에 대해서만 **바이패스** 인수 및 현재 변경 내용을 범위 지정 세션입니다. 이 명령을 실행해도 구성이 변경되지는 않습니다.
    
    `Set\-ExecutionPolicy Bypass \-Scope Process`

3. 인터넷 연결에 따라 다운로드하는 데 시간이 걸릴 수도 있습니다. 모든 파일이 다운로드되면 PowerShell 스크립트가  *DestDir*에 지정된 폴더에서 열립니다. PowerShell 명령 프롬프트에서 다음 명령을 실행하고 다운로드된 파일을 검토합니다.

    ```
    ls
    ```
**Results:**

![PowerShell 스크립트로 다운로드한 파일 목록](media/sqldev-python-filelist.png "PowerShell 스크립트로 다운로드한 파일 목록")

## <a name="next-step"></a>다음 단계

[2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>이전 단계

[In-database Python 분석 SQL 개발자를 위한](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>관련 항목:

[기계 학습 Python 사용 하 여 서비스](../python/sql-server-python-services.md)



