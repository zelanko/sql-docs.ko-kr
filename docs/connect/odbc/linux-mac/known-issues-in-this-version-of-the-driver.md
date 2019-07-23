---
title: 이 버전의 SQL Server용 드라이버에서 알려진 문제 | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3508277502ad7e3eb3b0e7ff048301c8ed1efdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008786"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>이 버전의 드라이버에서 알려진 문제

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서에는 Linux 및 macOS 기반 Microsoft ODBC Driver 13, 13.1 및 17 for SQL Server를 사용하는 경우 알려진 문제 목록이 포함되어 있습니다.

추가 문제는 [Microsoft ODBC 드라이버 팀 블로그](https://blogs.msdn.com/b/sqlnativeclient/)에 게시됩니다.  

- Windows, Linux 및 macOS는 PUA(프라이빗 사용 영역) 또는 EUDC(최종 사용자 정의)의 문자를 다르게 변환합니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 내에서 서버에 수행되는 변환은 Windows 변환 라이브러리를 사용합니다. 드라이버의 변환에는Windows, Linux 또는 macOS 변환 라이브러리를 사용합니다. 이러한 변환을 수행할 때 각 라이브러리는 다른 결과를 생성할 수 있습니다. 자세한 내용은 [최종 사용자 정의 및 프라이빗 사용 영역 문자](/windows/desktop/Intl/end-user-defined-characters)를 참조하세요.

- 클라이언트 인코딩이 UTF-8인 경우 드라이버 관리자가 항상 UTF-8에서 UTF-16으로 올바르게 변환하는 것은 아닙니다. 현재 문자열에서 1개 이상의 문자가 올바른 UTF-8 문자가 아닌 경우 데이터 손상이 발생합니다. ASCII 문자는 올바르게 매핑됩니다. ODBC API의 SQLCHAR 버전(예: SQLDriverConnectA)을 호출할 때 드라이버 관리자가 이 변환을 시도합니다. ODBC API의 SQLWCHAR 버전(예: SQLDriverConnectW)을 호출할 때 드라이버 관리자가 이 변환을 시도하지 않습니다.  

- **SQLBindParameter**의 *ColumnSize* 매개 변수는 SQL 형식의 문자 수를 가리키는 반면에, *BufferLength*는 애플리케이션의 버퍼에 있는 바이트 수입니다. 그러나 SQL 데이터 형식이 `varchar(n)` 또는 `char(n)`이고, 애플리케이션이 매개 변수를 SQL_C_CHAR 또는 SQL_C_VARCHAR로 바인딩하고, 클라이언트의 문자 인코딩이 UTF-8인 경우, *ColumnSize*의 값이 서버에서 데이터 형식의 크기와 정렬되는 경우에도 드라이버에서 "문자열 데이터의 오른쪽이 잘렸습니다"라는 오류를 받을 수 있습니다. 이 오류는 문자 인코딩 간 변환 시 데이터의 길이가 변경될 수 있기 때문에 발생합니다. 예를 들어 오른쪽 아포스트로피 문자(U+2019)는 CP-1252에서 1바이트 0x92로 인코딩되지만, UTF-8에서는 3바이트 시퀀스 0xe2 0x80 0x99로 인코딩됩니다.

예를 들어 사용하는 인코딩이 UTF-8인데 출력 매개 변수에 대해 **SQLBindParameter**의 *BufferLength* 및 *ColumnSize*에 모두 1을 지정한 다음, 서버에서 `char(1)` 열에 저장된 앞의 문자를 검색하려고(CP-1252를 사용하여) 시도하면 드라이버에서 해당 문자를 3바이트 UTF-8 인코딩으로 변환하지만 결과를 1바이트 버퍼에 맞출 수 없습니다. 반대 방향에서는 클라이언트 및 서버의 서로 다른 코드 페이지 간 변환을 수행하기 전에 *ColumnSize*를 **SQLBindParameter**의 *BufferLength*와 비교합니다. 예를 들어 *ColumnSize* 1은 *BufferLength* 3보다 작기 때문에 드라이버가 오류를 생성합니다. 이 오류를 방지하려면 변환 후의 길이가 지정된 버퍼 또는 열에 맞는지 확인합니다. *ColumnSize*는 `varchar(n)` 형식에 대해 8000보다 클 수 없습니다.

## <a name="see-also"></a>참고 항목  
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[릴리스 정보](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

