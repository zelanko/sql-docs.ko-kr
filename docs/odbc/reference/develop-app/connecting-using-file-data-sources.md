---
title: 파일 데이터 원본을 사용하여 연결 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287413"
---
# <a name="connecting-using-file-data-sources"></a>파일 데이터 원본을 사용하여 연결
파일 데이터 원본의 연결 정보는 .dsn 파일에 저장됩니다. 따라서 연결 문자열을 단일 사용자가 반복적으로 사용하거나 적절한 드라이버가 설치된 경우 여러 사용자 간에 공유할 수 있습니다. 파일에는 드라이버 이름(또는 공유할 수 없는 파일 데이터 원본의 경우 다른 데이터 원본 이름)과 **SQLDriverConnect**에서 사용할 수 있는 연결 문자열이 포함되어 있습니다. 드라이버 관리자는 .dsn 파일의 키워드에서 **SQLDriverConnect** 호출에 대한 연결 문자열을 작성합니다.  
  
 파일 데이터 원본을 사용하면 응용 프로그램에서 **SQLDriverConnect**에서 사용할 연결 문자열을 빌드하지 않고도 연결 옵션을 지정할 수 있습니다. 파일 데이터 원본은 일반적으로 **SAVEFILE** 키워드를 지정하여 만들어지며, 이로 인해 드라이버 관리자는 **SQLDriverConnect** 호출에 의해 생성된 출력 연결 문자열을 .dsn 파일에 저장합니다. 해당 연결 문자열은 **FILEDSN** 키워드로 **SQLDriverConnect를** 호출하여 반복적으로 사용할 수 있습니다. 이렇게 하면 연결 프로세스가 간소화되고 연결 문자열의 영구 소스가 제공됩니다.  
  
 파일 데이터 원본은 설치 프로그램 DLL에서 **SQLCreateDataSource를** 호출하여 만들 수도 있습니다. 정보는 **SQLWriteFileDSN을**호출하여 .dsn 파일에 쓸 수 있으며 **SQLReadFileDSN을**호출하여 .dsn 파일에서 읽을 수 있습니다. 이 두 기능은 모두 설치 프로그램 DLL에도 있습니다. 설치 관리자 DLL에 대한 자세한 내용은 [데이터 원본 구성을](../../../odbc/reference/install/configuring-data-sources.md)참조하십시오.  
  
 연결 정보에 사용되는 키워드는 .dsn 파일의 [ODBC] 섹션에 있습니다. 공유 가능한 .dsn 파일이 [ODBC] 섹션에 있는 최소 정보는 DRIVER 키워드입니다.  
  
```  
DRIVER = SQL Server  
```  
  
 공유 가능한 .dsn 파일에는 일반적으로 다음과 같이 연결 문자열이 포함되어 있습니다.  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 파일 데이터 원본을 공유할 수 없는 경우 .dsn 파일에는 **DSN** 키워드만 포함됩니다. 드라이버 관리자는 공유할 수 없는 파일 데이터 원본에서 정보를 보내면 필요에 따라 **DSN** 키워드로 표시된 데이터 원본에 연결됩니다. 공유할 수 없는 .dsn 파일에는 다음 키워드가 포함됩니다.  
  
```  
DSN = MyDataSource  
```  
  
 파일 데이터 원본에 사용되는 연결 문자열은 .dsn 파일에 지정된 키워드와 **SQLDriverConnect**호출의 연결 문자열에 지정된 키워드의 결합입니다. .dsn 파일의 키워드중 어느 것이 연결 문자열의 키워드와 충돌하는 경우 드라이버 관리자는 사용할 키워드 값을 결정합니다. 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
