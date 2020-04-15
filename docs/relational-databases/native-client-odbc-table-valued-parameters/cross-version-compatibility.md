---
title: 크로스 버전 호환성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7990072ac539addf733720fd8c1eaba0652f5d70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304516"
---
# <a name="cross-version-compatibility"></a>버전 간 호환성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]보다 이전 버전인 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 클라이언트 또는 서버 인스턴스에서 테이블 반환 매개 변수를 처리하는 경우 버전 간 충돌이 발생할 수 있습니다.  
  
 일반적으로 테이블 반환 매개 변수 기능은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 서버에 연결된 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 클라이언트(SQL Server Native Client 10.0 사용)에서만 사용할 수 있습니다. 카탈로그 함수 결과 집합의 새 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 열은(또는 이후) 서버에 연결된 경우에만 존재합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 이전 버전으로 컴파일된 클라이언트 애플리케이션이 테이블 반환 매개 변수가 필요한 문을 실행하면 서버에서 데이터 변환 오류를 통해 이 상태를 검색하며, ODBC에서 SQLSTATE 07006 및 &quot;제한된 데이터 형식 특성을 위반했습니다&quot;라는 메시지를 반환합니다.  
  
 네이티브 클라이언트 10.0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이상으로 컴파일된 클라이언트 응용 프로그램이 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]서버 인스턴스에 이전 보다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전에 연결될 때 테이블 값 매개 변수를 사용하려고 하면 네이티브 클라이언트가 이를 검색하고 SQLBindCol, SQLSetDesParameter, SQLSetDescState 및 SQLSetDescRec 호출은 "제한된 데이터 형식 특성 위반(이 연결에 대한 SQL Server 버전 은 해당 변수를 지원하지 않음)"이라는 메시지와 함께 실패합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 값 매개 변수](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
