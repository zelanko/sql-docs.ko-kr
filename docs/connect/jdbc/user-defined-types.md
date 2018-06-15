---
title: 사용자 정의 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72dca79e295f54d4c01421ef79408008bd559210
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850306"
---
# <a name="user-defined-types"></a>사용자 정의 형식
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  사용자 정의 형식 (Udt)에 도입 된 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 개발자의 공용 언어 런타임 (CLR) 개체를 저장 하 여 서버의 스칼라 형식 시스템을 확장할 수 있도록는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. Udt는 여러 요소를 포함할 수와 단일 구성 된 일반적인 별칭 데이터 형식과 달리 동작이 있을 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 시스템 데이터 형식입니다. 이전에는 UDT의 최대 크기가 8KB로 제한되었습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)], 64kb 보다 큰 Udt에 대 한 지원이 추가 되었습니다. UserDefined 형식을 지정하는 경우 버전 3.0부터 JDBC 드라이버는 이제 64KB를 초과하는 UDT도 지원합니다.  
  
 8,000바이트보다 작거나 같은 UDT의 동작에는 변경된 사항이 없지만 이보다 큰 UDT도 지원되며 이 경우 크기가 "제한 없음"으로 보고됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
