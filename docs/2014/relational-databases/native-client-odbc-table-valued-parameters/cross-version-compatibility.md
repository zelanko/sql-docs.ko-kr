---
title: 버전 간 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: rothja
ms.author: jroth
ms.openlocfilehash: af434713946f5c568ee71644a7403f9496a8c16f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049714"
---
# <a name="cross-version-compatibility"></a>버전 간 호환성
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]보다 이전 버전인 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 클라이언트 또는 서버 인스턴스에서 테이블 반환 매개 변수를 처리하는 경우 버전 간 충돌이 발생할 수 있습니다.  
  
 일반적으로 테이블 반환 매개 변수 기능은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 서버에 연결된 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 클라이언트(SQL Server Native Client 10.0 사용)에서만 사용할 수 있습니다. 카탈로그 함수 결과 집합의 새 열은 이상 버전의 서버에 연결 된 경우에만 표시 됩니다 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 이전 버전으로 컴파일된 클라이언트 애플리케이션이 테이블 반환 매개 변수가 필요한 문을 실행하면 서버에서 데이터 변환 오류를 통해 이 상태를 검색하며, ODBC에서 SQLSTATE 07006 및 &quot;제한된 데이터 형식 특성을 위반했습니다&quot;라는 메시지를 반환합니다.  
  
 Native Client 10.0 이상 버전을 사용 하 여 컴파일된 클라이언트 응용 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보다 이전 버전의 서버 인스턴스에 연결 된 경우 테이블 반환 매개 변수를 사용 하려고 하면 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client에서이를 감지 하 고, SQLBindCol, SQLBindParameter, SQLSetDescFields 및 SQLSetDescRec 호출은 오류가 발생 하 고 SQLSTATE 07006 및 "제한 된 데이터 형식 특성 위반 (이 연결에 대 한 SQL Server 버전은 테이블 반환 매개 변수를 지원 하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 반환 매개 변수](table-valued-parameters-odbc.md)  
  
  
