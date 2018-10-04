---
title: '3 단계: 서버가 레코드 집합 (RDS 자습서)을 얻는 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15401f0121ead5125a96796a207a4a66f1ee9d1d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727911"
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>3단계: 서버가 레코드 집합을 가져옵니다(RDS 자습서).
서버 프로그램 연결 문자열 및 명령 텍스트를 사용 하 여 원하는 행에 대 한 데이터 원본 쿼리. ADO는 일반적으로이 검색 하는 데 사용 됩니다 **레코드 집합**이지만 OLE DB를 사용할 수와 같은 다른 Microsoft 데이터 액세스 인터페이스, 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 사용자 지정 서버 프로그램이 같습니다.  
  
```  
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>관련 항목  
 [4 단계: 서버가 레코드 집합 (RDS 자습서) 반환합니다.](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
