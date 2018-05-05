---
title: 파일 데이터 원본을 사용 하 여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c598ed0eff0bbc760406332779df7a2839f97849
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-using-file-data-sources"></a>파일 데이터 원본을 사용 하 여 연결
파일 데이터 원본에 대 한 연결 정보는.dsn 파일에 저장 됩니다. 결과적으로, 연결 문자열을 단일 사용자가 반복적으로 사용할 또는 적절 한 드라이버가 설치 되어 있는 경우 여러 사용자가 공유할 수 있습니다. 드라이버 이름 (또는 다른 데이터 원본 이름을 공유할 수 없는 파일 데이터 원본의 경우)을 포함 하는 파일 및에서 사용할 수 있는 연결 문자열이 필요에 따라 **SQLDriverConnect**합니다. 드라이버 관리자에 대 한 호출에 대 한 연결 문자열을 작성 **SQLDriverConnect** .dsn 파일의 키워드에서입니다.  
  
 파일 데이터 원본을 통해 사용 하도록 연결 문자열을 작성할 필요 없이 연결 옵션을 지정 하려면 응용 프로그램 **SQLDriverConnect**합니다. 파일 데이터 원본을 지정 하 여 일반적으로 만든는 **SAVEFILE** 키워드를 호출 하 여 만든 출력 연결 문자열을 저장 하는 드라이버 관리자를 **SQLDriverConnect** .dsn 파일에 있습니다. 연결 문자열 사용할 수 있도록 반복적으로 호출 하 여 **SQLDriverConnect** 와 **FILEDSN** 키워드입니다. 이 연결 프로세스를 간소화 하 고 연결 문자열의 영구 리소스를 제공 합니다.  
  
 파일 데이터 원본도 만들 수 있습니다를 호출 하 여 **SQLCreateDataSource** DLL 설치 관리자에서 합니다. 호출 하 여.dsn 파일에 정보를 쓸 수 있으며 **SQLWriteFileDSN**를 호출 하 여.dsn 파일에서 읽습니다 **SQLReadFileDSN**; DLL 설치 관리자에도 포함 되어 이러한 함수는 모두 합니다. 설치 프로그램 DLL에 대 한 정보를 참조 하십시오. [데이터 소스 구성](../../../odbc/reference/install/configuring-data-sources.md)합니다.  
  
 연결 정보에 사용 되는 키워드.dsn 파일의 [ODBC] 섹션에 있습니다. 공유할 수 있는.dsn 파일 [ODBC] 섹션에는 최소한의 정보는 DRIVER 키워드:  
  
```  
DRIVER = SQL Server  
```  
  
 일반적으로 공유할 수 있는.dsn 파일 연결 문자열을 다음과 같이 포함:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 파일 데이터 소스를 공유할 수 없을 때만.dsn 파일 포함 한 **DSN** 키워드입니다. 연결 하 여 지정 된 데이터 소스를 필요에 따라 드라이버 관리자를 공유할 수 없는 파일 데이터 원본에 정보를 보내는 경우는 **DSN** 키워드입니다. 공유할 수 없는.dsn 파일에는 다음 키워드가 포함 됩니다.  
  
```  
DSN = MyDataSource  
```  
  
 파일 데이터 원본에 사용 되는 연결 문자열은.dsn 파일에 지정 된 키워드와 개체에 대 한 호출에서 연결 문자열에 지정 된 키워드의 합집합 **SQLDriverConnect**합니다. .Dsn 파일에 대 한 키워드는 연결 문자열에는 키워드와 충돌 하는 경우 드라이버 관리자 사용 해야 하는 키워드 값을 결정 합니다. 자세한 내용은 참조 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [http://support.microsoft.com/kb/165866](http://support.microsoft.com/kb/165866)
