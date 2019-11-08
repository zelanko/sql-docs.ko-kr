---
title: IOpenRowset을 사용 하 여 행 집합 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd80b90a8c40551344773ab7c5e95a539c21eefb
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788988"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>IOpenRowset을 사용하여 행 집합 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음과 같은 제한 사항이 있는 **Iopenrowset:: OpenRowset** 메서드를 지원 합니다.  
  
-   데이터베이스 ID(DBID) 구조체에 *pTableID* 매개 변수가 가리키는 기본 테이블 또는 뷰를 지정해야 합니다.  
  
-   DBID *eKind* 멤버는 DBKIND_NAME을 나타내야 합니다.  
  
-   DBID *uName* 멤버는 기존의 기본 테이블 또는 뷰 이름을 유니코드 문자열로 지정해야 합니다.  
  
-   *OpenRowset*의 **pIndexID** 매개 변수는 NULL이어야 합니다.  
  
 **IOpenRowset::OpenRowset**의 결과 집합에는 단일 행 집합이 들어 있습니다. 단일 행 집합을 포함하는 결과 집합은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서에서 지원될 수 있습니다. 커서 지원을 통해 개발자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동시성 메커니즘을 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
