---
title: 파일 데이터 원본을 사용 하 여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6fec2cea71ba818e955e0b6c2ce31c58f2c07357
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043888"
---
# <a name="connecting-using-file-data-sources"></a>파일 데이터 원본을 사용하여 연결
파일 데이터 원본에 대 한 연결 정보를.dsn 파일에 저장 됩니다. 결과적으로, 연결 문자열을 단일 사용자가 반복적으로 사용 하거나 적절 한 드라이버를 설치할 경우 여러 사용자가 공유 수 있습니다. 드라이버 이름 (또는 공유할 수 없는 파일 데이터 소스는 경우 다른 데이터 원본 이름)을 포함 하는 파일 및 필요에 따라 연결 문자열을 사용할 수 있는 **SQLDriverConnect**합니다. 드라이버 관리자에 대 한 호출에 대 한 연결 문자열을 빌드합니다 **SQLDriverConnect** .dsn 파일의 키워드에서.  
  
 파일 데이터 원본을 응용 프로그램 사용에 대 한 연결 문자열을 작성 하지 않고도 연결 옵션을 지정할 수 있습니다 **SQLDriverConnect**합니다. 파일 데이터 원본을 지정 하 여 일반적으로 만든 합니다 **SAVEFILE** 키워드를 호출 하 여 만든 출력 연결 문자열을 저장 하려면 드라이버 관리자를 사용 하면 **SQLDriverConnect** .dsn 파일. 호출 하 여 연결 문자열을 반복적으로 사용할 수 있습니다 **SQLDriverConnect** 사용 하 여 합니다 **FILEDSN** 키워드입니다. 이 연결 프로세스를 간소화 하 고 연결 문자열의 영구 리소스를 제공 합니다.  
  
 파일 데이터 원본을 만들 수도 있습니다를 호출 하 여 **SQLCreateDataSource** 설치 관리자 DLL에서에서. 호출 하 여.dsn 파일에 정보를 쓸 수 있으며 **SQLWriteFileDSN**를 호출 하 여.dsn 파일에서 읽고 **SQLReadFileDSN**; 설치 관리자 DLL에에서도 포함 되어 이러한 함수는 모두입니다. 설치 관리자 DLL에 대 한 정보를 참조 하세요 [데이터 원본 구성](../../../odbc/reference/install/configuring-data-sources.md)합니다.  
  
 연결 정보에 대 한 사용 된 키워드.dsn 파일의 [ODBC] 섹션에 있습니다. 최소한의 정보를 공유할 수 있는.dsn 파일 [ODBC] 섹션에는 DRIVER 키워드 같습니다.  
  
```  
DRIVER = SQL Server  
```  
  
 공유할 수 있는.dsn 파일을 일반적으로 연결 문자열을를 다음과 같이 포함:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 파일 데이터 소스를 공유할 수 없는 경우.dsn 파일을 포함 한 **DSN** 키워드입니다. 드라이버 관리자를 공유할 수 없는 파일 데이터 원본에 정보를 보내는 경우에 나타난 데이터 원본에 필요에 따라 연결 합니다 **DSN** 키워드입니다. 원본은.dsn 파일을 다음 키워드가 포함 됩니다.  
  
```  
DSN = MyDataSource  
```  
  
 파일 데이터 원본에 사용 되는 연결 문자열은.dsn 파일에 지정 된 키워드 및 호출에서 연결 문자열에 지정 된 키워드의 합집합 **SQLDriverConnect**합니다. 키워드.dsn 파일에서 연결 문자열 키워드를 사용 하 여 충돌 하는 경우 드라이버 관리자는 키워드 값을 사용할지 결정 합니다. 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
