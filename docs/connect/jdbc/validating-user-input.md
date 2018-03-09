---
title: "사용자 입력 유효성 검사 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a00eafc9f72910f05c1850b25bba5e91a4e276a6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="validating-user-input"></a>사용자 입력 유효성 검사
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터에 액세스하는 응용 프로그램을 만드는 경우 모든 사용자 입력은 입증되기 전까지 악의적일 수 있다고 가정해야 합니다. 그렇지 않으면 응용 프로그램이 쉽게 공격 당할 수 있습니다. 한 가지 유형의 발생할 수 있는 공격 라고 SQL 삽입의 인스턴스에 나중에 전달 되는 문자열에 악성 코드가 추가 여기서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문 분석 하 고 실행 합니다. 이러한 공격 유형을 피하기 위해 가능한 한 매개 변수와 함께 저장 프로시저를 사용해야 하고 항상 사용자 입력의 유효성을 검사해야 합니다.  
  
 서버로의 반복 이동으로 인한 시간을 절약할 수 있으므로 클라이언트 코드에서 사용자 입력의 유효성 검사는 중요합니다. 또한 유효하지 않고 클라이언트측 유효성을 무시하는 입력을 catch하기 위해 서버의 저장 프로시저에 대한 매개 변수의 유효성 검사도 중요합니다.  
  
 SQL 삽입 및 방지 하는 방법에 대 한 자세한 내용은 "SQL 삽입"의 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서. 저장된 프로시저 매개 변수 유효성을 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오. "저장 프로시저 ([!INCLUDE[ssDE](../../includes/ssde_md.md)])"의 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 응용 프로그램 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
