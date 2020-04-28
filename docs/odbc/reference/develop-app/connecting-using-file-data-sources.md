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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c752fc3b09c06c68dcc216cacac63744dc3101b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287413"
---
# <a name="connecting-using-file-data-sources"></a>파일 데이터 원본을 사용하여 연결
파일 데이터 원본에 대 한 연결 정보는 dsn 파일에 저장 됩니다. 따라서 단일 사용자가 연결 문자열을 반복 해 서 사용 하거나 적절 한 드라이버가 설치 된 경우 여러 사용자 간에 공유할 수 있습니다. 파일에는 드라이버 이름 (또는 unshareable 파일 데이터 원본의 경우 다른 데이터 원본 이름)이 포함 되 고, 선택적으로 **SQLDriverConnect**에서 사용할 수 있는 연결 문자열이 포함 됩니다. 드라이버 관리자는 **SQLDriverConnect** 에 대 한 호출에 대 한 연결 문자열을 dsn 파일의 키워드에서 빌드합니다.  
  
 응용 프로그램은 파일 데이터 원본을 사용 하 여 **SQLDriverConnect**와 함께 사용할 연결 문자열을 만들지 않고도 연결 옵션을 지정할 수 있습니다. 일반적으로 파일 데이터 원본은 **SAVEFILE** 키워드를 지정 하 여 생성 됩니다 .이를 통해 드라이버 관리자는 **SQLDriverConnect** 에 대 한 호출로 생성 된 출력 연결 문자열을 dsn 파일에 저장 합니다. 이 연결 문자열은 **Filedsn** 키워드와 함께 **SQLDriverConnect** 를 호출 하 여 반복 해 서 사용할 수 있습니다. 이렇게 하면 연결 프로세스가 간소화 되 고 연결 문자열의 영구적 소스가 제공 됩니다.  
  
 파일 데이터 소스는 설치 관리자 DLL에서 **Sqlcreatedatasource** 를 호출 하 여 만들 수도 있습니다. **Sqlwritefiledsn**을 호출 하 여 dsn 파일에 정보를 기록 하 고 **sqlwritefiledsn**을 호출 하 여 dsn 파일에서 읽을 수 있습니다. 이러한 함수는 모두 설치 관리자 DLL에도 있습니다. 설치 관리자 DLL에 대 한 자세한 내용은 [데이터 원본 구성](../../../odbc/reference/install/configuring-data-sources.md)을 참조 하세요.  
  
 연결 정보에 사용 되는 키워드는 dsn 파일의 [ODBC] 섹션에 있습니다. [ODBC] 섹션에 있는 공유 가능 dsn 파일의 최소 정보는 DRIVER 키워드입니다.  
  
```  
DRIVER = SQL Server  
```  
  
 일반적으로 공유 가능한 dsn 파일은 다음과 같이 연결 문자열을 포함 합니다.  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 파일 데이터 원본이 unshareable 인 경우 dsn 파일에는 **dsn** 키워드만 포함 됩니다. 드라이버 관리자가 unshareable 파일 데이터 원본에 정보를 보내면 **DSN** 키워드에 지정 된 데이터 원본에 필요에 따라 연결 됩니다. Unshareable 파일에는 다음 키워드가 포함 됩니다.  
  
```  
DSN = MyDataSource  
```  
  
 파일 데이터 원본에 사용 되는 연결 문자열은 dsn 파일에 지정 된 키워드와 **SQLDriverConnect**에 대 한 호출의 연결 문자열에 지정 된 키워드의 합집합입니다. Dsn 파일의 키워드가 연결 문자열의 키워드와 충돌 하는 경우 드라이버 관리자는 사용할 키워드 값을 결정 합니다. 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
