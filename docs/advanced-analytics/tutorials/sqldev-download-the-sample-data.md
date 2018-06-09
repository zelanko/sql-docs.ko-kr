---
title: 샘플 데이터를 다운로드 하는 1 단원 및 스크립트에 대 한 포함 된 R (SQL Server 기계 학습) | Microsoft Docs
description: SQL Server에서 R을 포함 하는 방법을 보여 주는 자습서 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 74a60a95da4fb701f3862c36e35a4bada6ef933b
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249836"
---
# <a name="lesson-1-download-data-and-scripts"></a>1 단원: 데이터와 스크립트를 다운로드 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 샘플 데이터 집합을 다운로드 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트이 자습서에 사용 되는 파일입니다. GitHub에서 공유 데이터와 스크립트 파일을 모두 있지만 PowerShell 스크립트를 로컬 디렉터리를 선택 해 데이터 및 스크립트 파일을 다운로드 합니다.

## <a name="download-tutorial-files-from-github"></a>Github에서 자습서 파일을 다운로드 합니다.

1.  Windows PowerShell 명령 콘솔을 엽니다.
  
    대상 디렉터리를 만들거나 지정된 대상에 파일을 쓰려면 관리자 권한이 필요한 경우 **관리자 권한으로 실행**옵션을 사용합니다.
  
2.  *DestDir* 매개 변수 값을 로컬 디렉터리로 변경하여 다음 PowerShell 명령을 실행합니다.  여기서 사용한 기본값은 **TempRSQL**입니다.
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    *DestDir* 에 지정한 폴더가 존재하지 않을 경우 PowerShell 스크립트를 통해 생성됩니다.
  
    > [!TIP]
    > 오류가 발생할 경우 Bypass 인수를 사용하고 변경 범위를 현재 세션으로 지정하여 이 연습에 대해서만 PowerShell 스크립트 실행 정책을 일시적으로 **무제한** 으로 설정할 수 있습니다.
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > 이 명령을 실행해도 구성이 변경되지는 않습니다.
  
    인터넷 연결에 따라 다운로드하는 데 시간이 걸릴 수도 있습니다.
  
3.  모든 파일이 다운로드되면 PowerShell 스크립트가  *DestDir*에 지정된 폴더에서 열립니다. PowerShell 명령 프롬프트에서 다음 명령을 실행하고 다운로드된 파일을 검토합니다.
  
    ```
    ls
    ```
  
    **Results:**
  
    ![PowerShell 스크립트로 다운로드한 파일 목록](media/rsql-devtut-filelist.png "PowerShell 스크립트로 다운로드한 파일 목록")
  
## <a name="next-lesson"></a>다음 단원

[2 단원: SQL server PowerShell을 사용 하 여 데이터 가져오기](../r/sqldev-import-data-to-sql-server-using-powershell.md)

## <a name="previous-lesson"></a>이전 단원

[SQL 개발자를 위해 포함 된 R 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)
