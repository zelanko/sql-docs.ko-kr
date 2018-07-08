---
title: 'Icommand:: Execute를 사용 하 여 행 집합 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1580beda75afbbacf9b600dd3b40bfe4e7c9d786
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410332"
---
# <a name="creating-rowsets-with-icommandexecute"></a>ICommand::Execute를 사용하여 행 집합 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  행 집합을 사용 하 여 만들 합니다 **icommand:: Execute** 메서드, 결과 행 집합에서 원하는 속성 명령의 텍스트를 제한할 수 있습니다. 이는 동적 명령 텍스트를 지원하는 고객에게 특히 중요합니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용할 수 없습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 많은 명령을 통해 생성 되는 여러 행 집합 결과 지원 하기 위해 커서입니다. 고객이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서 지원을 필요로 하는 행 집합을 요청할 경우 명령 텍스트가 둘 이상의 행 집합을 해당 결과로 생성하면 오류가 발생합니다. 자세한 내용은 [여러 행 집합 결과 생성 하는 명령을](../../relational-databases/native-client-ole-db-commands/commands-generating-multiple-rowset-results.md)합니다.  
  
 스크롤 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 행 집합에서 지 원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 데이터베이스의 다른 사용자가 변경한 내용의 영향을 받는 커서에 제한을 설정합니다. 특히 일부 커서의 행을 정렬할 수 없기 때문에 SQL ORDER BY 절이 포함된 명령을 사용하여 행 집합을 만들려고 하면 작업이 실패할 수 있습니다. 자세한 내용은 [행 집합 및 SQL Server 커서](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
