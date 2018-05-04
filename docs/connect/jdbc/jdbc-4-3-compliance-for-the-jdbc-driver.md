---
title: JDBC 4.3 JDBC 드라이버에 대 한 준수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be781d51418184aa519854c1ebd6bb59c19ff5b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 JDBC 드라이버에 대 한 준수
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  SQL Server 용 Microsoft JDBC 드라이버 6.4 이전 버전은 Java Database Connectivity API 4.2 사양에 대 한 규정을 준수 합니다. 이 섹션은 버전 6.4 릴리스 이전의 적용 되지 않습니다.  
  
 현재 SQL Server 용 Microsoft JDBC 드라이버 6.4에서 Java를 9 호환 가능 하지만 Java 데이터베이스 연결 API 4.3 사양에 대 한 완전 하 게 따르지 않습니다. 새로 JDBC 4.3의 Api를 도입 합니다. 그렇지 않은 경우 드라이버에서 지원에 대 한 드라이버는 SQLFeatureNotSupportedException throw 됩니다.