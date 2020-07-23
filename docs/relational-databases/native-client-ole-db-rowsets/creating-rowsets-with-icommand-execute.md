---
title: 'ICommand:: Execute (Native Client OLE DB provider)를 사용 하 여 행 집합 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86d8d14ccf50a0a0541eff8c9d16c738c66d8863
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942245"
---
# <a name="creating-rowsets-with-icommandexecute"></a>ICommand::Execute를 사용하여 행 집합 만들기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **ICommand::Execute** 메서드를 사용하여 행 집합을 만들 경우 결과 행 집합의 속성에 의해 명령 텍스트가 제한될 수 있습니다. 이는 동적 명령 텍스트를 지원하는 고객에게 특히 중요합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서를 사용 하 여 여러 명령으로 생성 된 다중 행 집합 결과를 지원할 수 없습니다. 고객이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서 지원을 필요로 하는 행 집합을 요청할 경우 명령 텍스트가 둘 이상의 행 집합을 해당 결과로 생성하면 오류가 발생합니다. 자세한 내용은 [여러 행 집합 결과를 생성하는 명령](../../relational-databases/native-client-ole-db-commands/commands-generating-multiple-rowset-results.md)을 참조하세요.  
  
 스크롤할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 수 있는 Native Client OLE DB 공급자 행 집합은 커서에서 지원 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 데이터베이스의 다른 사용자가 변경한 내용의 영향을 받는 커서에 제한을 설정합니다. 특히 일부 커서의 행을 정렬할 수 없기 때문에 SQL ORDER BY 절이 포함된 명령을 사용하여 행 집합을 만들려고 하면 작업이 실패할 수 있습니다. 자세한 내용은 [행 집합 및 SQL Server 커서](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
