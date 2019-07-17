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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a3156c3f71eb4b3f7b8319da5d5fec7514f08b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087963"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 열 크기(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 를 열고 Oracle8에서 VARCHAR 열 최대 크기인 4000 바이트를 2000에서 증가 했습니다. Oracle 7.3.x 클라이언트 소프트웨어는 2000 바이트 보다 큰 매개 변수 값에 바인딩할 수 없습니다. 따라서 2000 바이트 보다 클 때는 VARCHAR 열과 테이블을 만든 경우 있습니다 됩니다 수 없습니다 매개 변수가 있는 삽입, 업데이트, 삭제 및 클라이언트 소프트웨어의 2000 바이트 제한을 초과 하는 데이터를 사용 하 여 쿼리를 수행 하려면. Oracle 용 ODBC 드라이버와 OLE DB Provider for Oracle 모두 매개 변수화 된 삽입, 업데이트, 삭제 및 쿼리를 사용 하므로 경우 ORA-01026 오류 보고 됩니다. Oracle 클라이언트 소프트웨어에 의해 적용 된 제한 내에 있는 데이터 작동 합니다. 이 2000 바이트 한계를 방지 하려면 열고 Oracle8에 클라이언트 소프트웨어를 업그레이드 해야 합니다 (8.0.4.1.1c 이상).
