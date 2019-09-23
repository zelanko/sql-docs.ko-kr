---
title: SSMS(SQL Server Management Studio)의 중단 또는 충돌 문제 해결
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 07/01/2019
ms.openlocfilehash: e73e3d8cc0b54f0251530327dbcea941546471d5
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212442"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>SSMS(SQL Server Management Studio) 충돌이 발생한 후 진단 데이터 가져오기

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-after-a-hang-or-crash"></a>중단 또는 충돌 후 전체 메모리 덤프 가져오기

중단되거나 충돌할 때 SSMS(SQL Server Management Studio)의 전체 메모리 덤프를 가져옵니다.

SSMS의 충돌 또는 중단 문제를 해결하기 위한 진단 정보를 캡처하려면 아래 단계를 따르세요.

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)를 다운로드합니다.

2. 폴더에서 다운로드 파일의 압축을 풉니다.

3. 명령 프롬프트를 열고 다음 명령을 실행합니다.

    ```console
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    사용권 계약 수락을 요청하는 메시지가 표시되면 *동의*를 선택합니다.

4. SSMS를 아직 시작하지 않은 경우 시작합니다.

5. 이슈를 재현합니다.

6. 덤프 파일을 작성하기 위해 텍스트에 cmd 프롬프트가 나타납니다. 작성이 완료될 때까지 기다리세요.

7. 새 폴더를 만들고 작성된 폴더의 *.dmp 파일을 복사합니다.

8. 다음 파일을 동일한 폴더에 복사합니다.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. 폴더 압축

## <a name="get-full-memory-dump-for-an-outofmemoryexception"></a>OutOfMemoryException에 대한 전체 메모리 덤프 가져오기

OutOfMemoryException을 throw할 때 SSMS의 전체 메모리 덤프를 가져옵니다.

모든 관리형 예외가 발생한 전체 메모리 덤프를 가져올 수 있습니다.

SSMS에서 OutOfMemoryException 문제를 해결하기 위한 진단 정보를 캡처하려면 아래 단계를 따르세요.

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)를 다운로드합니다.

2. 폴더에서 다운로드 파일의 압축을 풉니다.

3. 명령 프롬프트를 열고 다음 명령을 실행합니다.

    ```console
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    사용권 계약 수락을 요청하는 메시지가 표시되면 *동의*를 선택합니다.

4. 아직 시작하지 않은 경우 SQL Server Management Studio를 시작합니다.

5. 이슈를 재현합니다.

6. 덤프 파일을 작성하기 위해 텍스트에 cmd 프롬프트가 나타납니다. 작성이 완료될 때까지 기다리세요.

7. 새 폴더를 만들고 작성된 폴더의 *.dmp 파일을 복사합니다.

8. 다음 파일을 동일한 폴더에 복사합니다.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. 폴더를 압축합니다.
