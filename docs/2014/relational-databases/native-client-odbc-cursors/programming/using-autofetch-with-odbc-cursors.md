---
title: ODBC 커서와 함께 자동 인출 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: rothja
ms.author: jroth
ms.openlocfilehash: e3d9374cf9ceab4a7e73cc0059783486f2bf9c41
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020757"
---
# <a name="using-autofetch-with-odbc-cursors"></a>ODBC 커서로 자동 인출 사용
  인스턴스에 연결 된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버는 서버 커서 유형을 사용할 때 자동 인출 옵션을 지원 합니다. 자동 인출를 사용 하면 커서를 여는 **Sqlexecute** 또는 **sqlexecdirect** 함수에도 암시적 [sqlfetchscroll](../../native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) 함수가 있습니다. 문 실행의 일부로 첫 번째 행 집합을 구성하는 행이 바인딩된 애플리케이션 변수에 반환되므로 네트워크를 통해 다시 서버로 왕복할 필요가 없습니다. 자동 인출 옵션을 사용 하는 경우 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 는 지원 되지 않습니다. 결과 집합 열은 프로그램 변수에 바인딩되어야 합니다.  
  
 애플리케이션은 드라이버별 SQL_SOPT_SS_CURSOR_OPTIONS 문 특성을 SQL_CO_AF로 설정하여 자동 인출을 요청합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 프로그래밍 정보](cursor-programming-details-odbc.md)  
  
  
