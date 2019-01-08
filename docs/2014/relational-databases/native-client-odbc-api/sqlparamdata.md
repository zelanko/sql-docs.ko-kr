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
ms.openlocfilehash: da50163b90d4a871c2524e1723797474386be8f6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356209"
---
# <a name="sqlparamdata"></a>SQLParamData
  SQLParamData 반환 하는 경우는 *ValuePtrPtr* 테이블 반환 매개 변수를 사용 하 여 연결, 응용 프로그램 호출 해야 사용 하 여 SQLPutData *StrLen_Or_Ind*합니다. *StrLen_Or_Ind* 의 값이 0보다 크면 애플리케이션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 다음 테이블 반환 매개 변수에 대한 데이터를 수집할 준비가 되었음을 나타냅니다. *StrLen_Or_Ind* 의 값이 0이면 테이블 반환 매개 변수에 대한 데이터의 행이 더 이상 없음을 나타냅니다. 자세한 내용은 [바인딩 및 Data Transfer of Table-Valued 매개 변수 및 열 값](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
