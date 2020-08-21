---
title: SQLDriverConnect를 사용 하 여 연결 | Microsoft Docs
description: SQLDriverConnect는 사용자에 게 자세한 정보를 표시 하는 옵션을 포함 하 여 SQLConnect에 대 한 추가 연결 기능을 제공 합니다.
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78186e903405aa1b59cfac185e62646dbda6e77a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746173"
---
# <a name="connecting-with-sqldriverconnect"></a>SQLDriverConnect로 연결

**SQLDriverConnect** 는 연결 문자열을 사용 하 여 데이터 원본에 연결 하는 데 사용 됩니다. 다음 시나리오에서는 **SQLConnect** 대신 **SQLDriverConnect** 를 사용 합니다.  
  
- 데이터 원본 이름, 하나 이상의 사용자 Id, 하나 이상의 암호 및 데이터 원본에 필요한 기타 정보를 포함 하는 연결 문자열을 사용 하 여 연결을 설정 합니다.  
  
- 부분 연결 문자열 또는 추가 정보를 사용 하 여 연결을 설정 합니다. 이 경우 드라이버 관리자와 드라이버는 각각 사용자에 게 연결 정보를 묻는 메시지를 표시할 수 있습니다.  
  
- 시스템 정보에 정의 되어 있지 않은 데이터 원본에 대 한 연결을 설정 합니다. 응용 프로그램에서 부분 연결 문자열을 제공 하는 경우 드라이버는 사용자에 게 연결 정보를 묻는 메시지를 표시할 수 있습니다.  
  
- Dsn 파일의 정보에서 생성 된 연결 문자열을 사용 하 여 데이터 원본에 대 한 연결을 설정 합니다.  
  
연결이 설정 된 후 **SQLDriverConnect** 는 완료 된 연결 문자열을 반환 합니다. 응용 프로그램은 후속 연결 요청에이 문자열을 사용할 수 있습니다.

이 섹션에서는 다음 항목을 다룹니다.  
  
- [드라이버별 연결 정보](driver-specific-connection-information.md)  
  
- [사용자에게 연결 정보 요청](prompting-the-user-for-connection-information.md)  
  
- [파일 데이터 원본을 사용하여 연결](connecting-using-file-data-sources.md)  
  
- [드라이버에 직접 연결](connecting-directly-to-drivers.md)
