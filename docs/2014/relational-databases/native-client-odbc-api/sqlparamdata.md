---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e574813485809825beec661721c8b7e0ccbe77ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056743"
---
# <a name="sqlparamdata"></a>SQLParamData
  SQLParamData 반환 하는 경우는 *ValuePtrPtr* 테이블 반환 매개 변수를 사용 하 여 연결, 응용 프로그램 호출 해야 사용 하 여 SQLPutData *StrLen_Or_Ind*합니다. 하는 경우 *StrLen_Or_Ind* 값이 0 보다 큰 응용 프로그램에 대 한 준비 되어 있다는 뜻 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 다음 테이블 반환 매개 변수 행에 대 한 매개 변수 데이터를 수집 하도록 합니다. *StrLen_Or_Ind* 의 값이 0이면 테이블 반환 매개 변수에 대한 데이터의 행이 더 이상 없음을 나타냅니다. 자세한 내용은 [바인딩 및 Data Transfer of Table-Valued 매개 변수 및 열 값](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
