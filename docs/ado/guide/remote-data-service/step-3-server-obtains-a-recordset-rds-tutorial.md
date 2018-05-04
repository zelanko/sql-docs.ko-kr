---
title: '3 단계: 서버 가져옵니다 (RDS 자습서) 레코드 집합 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdefc86152b1a91ab20099e31a748940c5fe57ff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>3 단계: 서버가 가져옵니다 (RDS 자습서) 레코드 집합을
서버 프로그램 연결 문자열 및 명령 텍스트를 사용 하 여 원하는 행에 대 한 데이터 원본을 쿼리할 수 있습니다. ADO는 일반적으로 검색 하는 데이 **레코드 집합**OLE DB를 사용할 수와 같은 다른 Microsoft 데이터 액세스 인터페이스, 하지만, 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 사용자 지정 서버 프로그램은 다음과 같이 표시 될 수 있습니다.  
  
```  
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>관련 항목:  
 [4 단계: 서버 반환 레코드 집합 (RDS 자습서)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
