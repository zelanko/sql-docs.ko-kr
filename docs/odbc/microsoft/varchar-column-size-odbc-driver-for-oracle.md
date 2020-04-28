---
title: VARCHAR 열 크기 (Oracle 용 ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e1de3171521c57c80beb207d33e67d26d3e33
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304828"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 열 크기(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle8에서 VARCHAR 열의 최대 크기는 2000에서 4000 바이트로 증가 했습니다. Oracle 7.3 클라이언트 소프트웨어는 2000 바이트 보다 큰 매개 변수 값을 바인딩할 수 없습니다. 따라서 VARCHAR 열이 2000 바이트 보다 큰 테이블을 만드는 경우 클라이언트 소프트웨어의 2000 바이트 제한을 초과 하는 데이터를 사용 하 여 매개 변수가 있는 삽입, 업데이트, 삭제 및 쿼리를 수행할 수 없습니다. Oracle 용 ODBC 드라이버와 Oracle 용 OLE DB 공급자는 모두 매개 변수가 있는 삽입, 업데이트, 삭제 및 쿼리를 사용 하기 때문에이 경우 ORA-01026 오류를 보고 합니다. Oracle 클라이언트 소프트웨어에 의해 적용 되는 제한 범위 내에 있는 데이터는 작동 합니다. 이 2000 바이트 제한을 방지 하려면 클라이언트 소프트웨어를 Oracle8 (8.0.4.1.1 c 이상)로 업그레이드 해야 합니다.
