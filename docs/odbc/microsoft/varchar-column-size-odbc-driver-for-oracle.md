---
title: "VARCHAR 열 크기 (ODBC Driver for Oracle) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57dcc53769c9b5ba80f5c949436f0b3eb2ce08b1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 열 크기 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 열고 Oracle8, VARCHAR 열의 최대 크기는 4, 000 바이트로 2000에서 증가 했습니다. Oracle 7.3.x 클라이언트 소프트웨어는 2000 바이트 보다 큰 매개 변수 값에 바인딩할 수 없습니다. 따라서 2000 바이트 보다 큰의 VARCHAR 열이 있는 테이블을 만들 경우 수 없게 됩니다 매개 변수화 된 삽입, 업데이트, 삭제 및 클라이언트 소프트웨어의 2000 바이트 제한을 초과 하는 데이터에 대 한 쿼리를 수행 하 합니다. Oracle에 대 한 ODBC 드라이버와 OLE DB Provider for Oracle 모두 매개 변수화 된 삽입, 업데이트, 삭제 및 쿼리를 사용 하므로 이러한에서 오류를 보고 또는 01026이 경우. Oracle 클라이언트 소프트웨어에 의해 적용 된 제한 내 데이터 작동 합니다. 2000 바이트 제한을이 방지 하려면 열고 Oracle8에 클라이언트 소프트웨어를 업그레이드 해야 합니다 (8.0.4.1.1c 또는 이상)입니다.

