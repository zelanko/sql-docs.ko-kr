---
title: SQL Server 용 드라이버의이 버전의 알려진 문제 | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- known issues
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cd3bb6f733b9d9cac1dc3973e65199c9357bbbb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="known-issues-in-this-version-of-the-driver"></a>이 버전의 드라이버에서 알려진 문제

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서에는 Microsoft ODBC Driver 13, 13.1, 및 SQL Server에 대 한 17 Linux와 macOS에서의 알려진된 문제 목록이 포함 되어 있습니다.

추가 문제는 [Microsoft ODBC 드라이버 팀 블로그](http://blogs.msdn.com/b/sqlnativeclient/)에 게시됩니다.  

- Windows, Linux 및 macOS 문자를 다르게 개인 사용 영역 (PUA) 또는 최종 EUDC ()에서 변환합니다. 변환 내에서 서버에 수행 [!INCLUDE[tsql](../../../includes/tsql_md.md)] Windows 변환 라이브러리를 사용 합니다. 드라이버의 변환은 Windows, Linux 또는 macOS 변환 라이브러리를 사용 합니다. 각 라이브러리는 이러한 변환을 수행할 때 다른 결과가 발생할 수 있습니다. 자세한 내용은 [최종 사용자 정의 및 개인 사용자 영역 문자](http://msdn.microsoft.com/library/dd317802.aspx)를 참조하세요.

- 인코딩이 u t F-8 이면 드라이버 관리자는 변환 하지 않습니다 올바르게 항상 u t F-8에서 u t F-16으로. 현재 문자열에서 하나 이상의 문자 올바른 utf-8 문자가 없는 경우 데이터 손상이 발생 합니다. ASCII 문자는 제대로 매핑됩니다. 드라이버 관리자 (예: SQLDriverConnectA)는 ODBC API의 SQLCHAR 버전을 호출할 때이 변환을 시도 합니다. ODBC API의 SQLWCHAR 버전(예: SQLDriverConnectW)을 호출할 때 드라이버 관리자가 이 변환을 시도하지 않습니다.  

- *ColumnSize* 의 매개 변수 **SQLBindParameter** SQL 형식에 있는 문자의 수를 참조 하는 동안 *BufferLength* 응용 프로그램의 바이트 수입니다 버퍼입니다. 그러나 SQL 데이터 형식이 `varchar(n)` 또는 `char(n)`, 응용 프로그램 매개 변수를 SQL_C_CHAR 또는 SQL_C_VARCHAR, 바인딩합니다 및 클라이언트의 문자 인코딩은 u t F-8입니다, 경우에도 드라이버에서 "문자열 데이터, 오른쪽이 잘렸습니다." 오류가 발생할 수 있습니다는 값 *ColumnSize* 서버에서 데이터 형식의 크기에 맞게 정렬 됩니다. 이 오류에는 문자 인코딩 간의 변환을 데이터의 길이 변경할 수 있으므로 발생 합니다. 예를 들어 오른쪽 아포스트로피 문자 (U + 2019)-1252 0x92, 단일 바이트 있지만 u t F-8에서 3 바이트 시퀀스 0xe2로 인코딩된 0x80 0x99 합니다.

예를 들어, 프로그램 인코딩이 u t F-8 둘 다에 대해 1을 지정 하는 경우 *BufferLength* 및 *ColumnSize* 에 **SQLBindParameter** out 매개 변수 및 하려면 에 저장 된 앞에 오는 문자를 검색 한 `char(1)` 열 (사용 하 여 c P-1252)는 서버의 드라이버 3 바이트 u t F-8 인코딩으로 변환 하려고 시도 하지만 1 바이트 버퍼에 결과 포함할 수 없습니다. 비교 반대 방향의 *ColumnSize* 와 *BufferLength* 에 **SQLBindParameter** 에 서로 다른 코드 페이지 간의 변환을 수행 하기 전에 클라이언트와 서버입니다. 예를 들어 *ColumnSize* 1은 *BufferLength* 3보다 작기 때문에 드라이버가 오류를 생성합니다. 이 오류를 방지 하려면 확인 하는 데이터의 길이 지정 된 버퍼 또는 열에 적합 한지 변환 후 합니다. *ColumnSize* 에 대해 8000 보다 클 수 없습니다는 `varchar(n)` 유형입니다.

## <a name="see-also"></a>관련 항목:  
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)  

