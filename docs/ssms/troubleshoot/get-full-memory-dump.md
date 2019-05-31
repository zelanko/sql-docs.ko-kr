---
title: SSMS(SQL Server Management Studio)의 문제를 해결하기 위한 전체 메모리 덤프 가져오기
Description: 전체 메모리 덤프를 수집하여 SSMS 중단 또는 크래시 문제 해결
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: how-to
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: dineth, sstein
ms.custom: ''
ms.date: 05/17/2019
ms.openlocfilehash: 2fbd0f4680c7a63a5390d93589f44b708f6c2629
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983124"
---
# <a name="get-full-memory-dump"></a>전체 메모리 덤프 가져오기

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

이 문서에서는 SSMS(SQL Server Management Studio)에서 발생한 크래시 또는 중단 문제를 해결하기 위한 진단 정보를 캡처하는 방법을 알아볼 수 있습니다.

문제를 해결하기 위한 진단 정보를 캡처하려면 아래 단계를 따르세요.

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)를 다운로드합니다.

2. 폴더에서 다운로드 파일의 압축을 풉니다.

3. 명령 프롬프트를 열고 다음 명령을 실행합니다.

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    사용권 계약 수락을 요청하는 메시지가 표시되면 **동의**를 선택합니다.

4. 아직 시작하지 않은 경우 SSMS(SQL Server Management Studio)를 시작합니다.

5. 문제를 재현합니다.

6. 덤프 파일을 작성하기 위해 텍스트에 cmd 프롬프트가 나타납니다. 작성이 완료될 때까지 기다리세요.

7. 새 폴더를 만들고 작성된 폴더의 *.dmp 파일을 복사합니다.

8. 다음 파일을 동일한 폴더에 복사합니다.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. 폴더를 압축합니다.

## <a name="outofmemoryexception"></a>OutOfMemoryException

OutOfMemoryException(관리되는 예외 모두 가능)을 throw할 때 SSMS의 전체 메모리 덤프를 가져올 수도 있습니다.

SSMS에서 OutOfMemoryException 문제를 해결하기 위한 진단 정보를 캡처하려면 아래 단계를 따르세요.

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)를 다운로드합니다.

2. 폴더에서 다운로드 파일의 압축을 풉니다.

3. 명령 프롬프트를 열고 다음 명령을 실행합니다.

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    사용권 계약 수락을 요청하는 메시지가 표시되면 **동의**를 선택합니다.

4. 아직 시작하지 않은 경우 SQL Server Management Studio를 시작합니다.

5. 문제를 재현합니다.

6. 덤프 파일을 작성하기 위해 텍스트에 cmd 프롬프트가 나타납니다. 작성이 완료될 때까지 기다리세요.

7. 새 폴더를 만들고 작성된 폴더의 *.dmp 파일을 복사합니다.

8. 다음 파일을 동일한 폴더에 복사합니다.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. 폴더를 압축합니다.

## <a name="share-the-information"></a>정보 공유

1. SSMS 팀과 정보를 공유하려면 https://aka.ms/sqlfeedback에 문제를 기록합니다.

2. 그런 다음, 수집된 메모리 덤프 파일을 파일이 수집될 수 있는 OneDrive(또는 이와 동등한)에 공유합니다.

    > [!Important]
    > 메모리 덤프 파일에는 중요한 정보가 들어 있을 수 있습니다.

## <a name="next-steps"></a>다음 단계

[SQL Server Management Studio](../sql-server-management-studio-ssms.md)