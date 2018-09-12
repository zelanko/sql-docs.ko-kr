---
title: 1 단계는 샘플 데이터 다운로드 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 07a9b5219649b370b0a5df1e53cf75765f18ec7f
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888321"
---
# <a name="step-1-download-the-sample-data"></a>1 단계: 샘플 데이터 다운로드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서에 일부 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

데이터와이 자습서에 대 한 스크립트는 Github에서 공유 됩니다. 이 단계에서는 PowerShell 스크립트를 사용 하 여 선택한 로컬 디렉터리에 데이터 및 스크립트 파일을 다운로드 합니다.

## <a name="run-the-script"></a>스크립트를 실행 합니다.

1. Windows PowerShell 명령 콘솔을 엽니다.

    옵션을 사용 하 여 **관리자 권한으로 실행**이면 대상 디렉터리를 만들거나 지정된 된 대상에 파일을 쓰려면 관리자 권한이 필요 합니다.

2. *DestDir* 매개 변수 값을 로컬 디렉터리로 변경하여 다음 PowerShell 명령을 실행합니다.  여기서 사용한 기본값은 `C:\temp\pysql`합니다.

    ```ps
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\temp\pysql'
    ```
    
    *DestDir* 에 지정한 폴더가 존재하지 않을 경우 PowerShell 스크립트를 통해 생성됩니다.
    
    설정 하는 PowerShell 스크립트의 실행 정책을 일시적으로 오류가 발생 하는 경우 **무제한** 사용 하 여이 연습에서는 합니다 **바이패스** 인수 및 현재 세션 변경의 범위를 지정 합니다. 이 명령을 실행해도 구성이 변경되지는 않습니다.
    
    ```ps
    Set-ExecutionPolicy Bypass -Scope Process
    ```

3. 인터넷 연결에 따라 다운로드 시간이 걸릴 수 있습니다. 

## <a name="view-results"></a>결과 보기

모든 파일이 다운로드되면 PowerShell 스크립트가  *DestDir*에 지정된 폴더에서 열립니다. 

+ PowerShell 명령 프롬프트에서 다운로드 된 파일을 나열 하려면 다음 명령을 실행 합니다.

    ```ps
    ls
    ```

![PowerShell 스크립트로 다운로드한 파일 목록](media/sqldev-python-filelist.png "PowerShell 스크립트로 다운로드한 파일 목록")

## <a name="next-step"></a>다음 단계

[2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>이전 단계

[데이터베이스 내 Python 분석 SQL 개발자를 위한](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>관련 항목

[SQL Server의 Python 확장](../concepts/extension-python.md)


