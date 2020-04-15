---
title: VARCHAR 열 크기 (오라클ODBC 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304828"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 열 크기(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 Oracle8에서 VARCHAR 열의 최대 크기가 2000바이트에서 4000바이트로 증가했습니다. Oracle 7.3.x 클라이언트 소프트웨어는 2000바이트보다 큰 매개 변수 값을 바인딩할 수 없습니다. 따라서 2000바이트보다 큰 VARCHAR 열을 가진 테이블을 만드는 경우 클라이언트 소프트웨어의 2000바이트 제한을 초과하는 데이터로 매개 변수화된 삽입, 업데이트, 삭제 및 쿼리를 수행할 수 없습니다. 오라클의 ODBC 드라이버와 오라클용 OLE DB 공급자모두 매개 변수화된 삽입, 업데이트, 삭제 및 쿼리를 사용하기 때문에 이 경우 ORA-01026 오류를 보고합니다. Oracle 클라이언트 소프트웨어가 적용하는 한도 내에 있는 데이터는 작동합니다. 이 2000바이트 제한을 피하려면 클라이언트 소프트웨어를 Oracle8(8.0.4.1.1c 이상)으로 업그레이드해야 합니다.
