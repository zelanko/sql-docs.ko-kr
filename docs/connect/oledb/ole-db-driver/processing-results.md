---
title: 결과 처리 | Microsoft Docs
description: 결과 처리
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0a07bdd4181e85bdbeeea7e3751613a860bc5754
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665353"
---
# <a name="processing-results"></a>결과 처리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  명령을 실행하거나 공급자에서 직접 행 집합 개체를 생성하여 행 집합 개체가 만들어진 경우 소비자가 행 집합의 데이터를 검색하여 액세스해야 합니다.  
  
 행 집합은 OLE DB 드라이버에서 테이블 형식 데이터를 노출 하도록 SQL Server를 사용 하도록 설정 하는 중앙 개체입니다. 개념상, 행 집합은 각 행이 열 데이터를 갖는 행의 집합입니다. 행 집합 개체와 같은 인터페이스를 노출 **IRowset** (순차적으로 행 집합에서 행을 인출 하기 위한 메서드 포함) **IAccessor** (의 테이블 형식 데이터가 소비자 프로그램 변수에 바인딩되는 방식을 설명 하는 열 바인딩 그룹의 정의 허용) **IColumnsInfo** (행 집합의 열에 대 한 정보 제공) 및 **IRowsetInfo** (행 집합에 대 한 정보 제공).  
  
 소비자는 호출할 수는 **irowset:: Getdata** 버퍼에 행 집합에서 데이터의 행을 검색 하는 메서드. 하기 전에 **GetData** 은 호출, 소비자는 DBBINDING 구조 집합을 사용 하 여 버퍼를 설명 합니다. 각 바인딩은 행 집합이 소비자 버퍼에 저장되는 방법을 설명하며 다음을 포함합니다.  
  
-   바인딩이 적용되는 열(또는 매개 변수)의 서수  
  
-   바인딩되는 항목에 대한 정보(예: 데이터 값, 데이터 길이 및 바인딩 상태)  
  
-   이러한 각 부분에 대한 버퍼의 오프셋 정보  
  
-   소비자 버퍼에 존재하는 데이터 값의 길이와 유형  
  
 데이터를 가져올 때 공급자는 각 바인딩의 정보를 사용하여 소비자 버퍼에서 데이터를 검색하는 위치와 방법을 확인합니다. 소비자 버퍼에 데이터를 설정하는 경우에는 각 바인딩의 정보를 사용하여 데이터를 소비자 버퍼에 반환하는 위치와 방법을 확인합니다.  
  
 DBBINDING 구조가 지정 된 후 접근자가 생성 됩니다 (**iaccessor:: Createaccessor**). 접근자는 바인딩 컬렉션으로, 소비자 버퍼의 데이터를 가져오거나 설정하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 응용 프로그램에 대 한 OLE DB 드라이버 만들기](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [OLE DB 방법 도움말 항목](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
