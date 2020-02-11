---
title: 결과 처리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [SQL Server Native Client]
ms.assetid: 20887ac4-f649-4e7f-92e6-f929e2e70952
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fdc66899f7d863cbfb3ae04ad0796614717a734
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63209669"
---
# <a name="processing-results"></a>결과 처리
  명령을 실행하거나 공급자에서 직접 행 집합 개체를 생성하여 행 집합 개체가 만들어진 경우 소비자가 행 집합의 데이터를 검색하여 액세스해야 합니다.  
  
 행 집합은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 데이터를 테이블 형식으로 노출할 수 있도록 하는 중앙 개체입니다. 개념상, 행 집합은 각 행이 열 데이터를 갖는 행의 집합입니다. 행 집합 개체는 **IRowset**(행 집합에서 순차적으로 행을 인출하기 위한 메서드 포함), **IAccessor**(테이블 형식 데이터가 소비자 프로그램 변수에 바인딩되는 방법을 설명하는 열 바인딩 그룹의 정의 허용), **IColumnsInfo**(행 집합의 열에 대한 정보 제공) 및 **IRowsetInfo**(행 집합에 대한 정보 제공)와 같은 인터페이스를 노출합니다.  
  
 소비자는 **IRowset::GetData** 메서드를 호출하여 행 집합의 데이터 행을 버퍼로 검색할 수 있습니다. 
  **GetData**를 호출하기 전에 소비자는 DBBINDING 구조 집합을 사용하여 버퍼를 설명합니다. 각 바인딩은 행 집합이 소비자 버퍼에 저장되는 방법을 설명하며 다음을 포함합니다.  
  
-   바인딩이 적용되는 열(또는 매개 변수)의 서수  
  
-   바인딩되는 항목에 대한 정보(예: 데이터 값, 데이터 길이 및 바인딩 상태)  
  
-   이러한 각 부분에 대한 버퍼의 오프셋 정보  
  
-   소비자 버퍼에 존재하는 데이터 값의 길이와 유형  
  
 데이터를 가져올 때 공급자는 각 바인딩의 정보를 사용하여 소비자 버퍼에서 데이터를 검색하는 위치와 방법을 확인합니다. 소비자 버퍼에 데이터를 설정하는 경우에는 각 바인딩의 정보를 사용하여 데이터를 소비자 버퍼에 반환하는 위치와 방법을 확인합니다.  
  
 DBBINDING 구조가 지정된 후 접근자가 생성됩니다(**IAccessor::CreateAccessor**). 접근자는 바인딩 컬렉션으로, 소비자 버퍼의 데이터를 가져오거나 설정하는 데 사용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client OLE DB 공급자 응용 프로그램 만들기](creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [OLE DB 방법 도움말 항목](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
