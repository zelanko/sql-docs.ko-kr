---
title: ICommand (OLE DB) | Microsoft Docs
description: ICommand 인터페이스 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 4ecb3b505d7da116711bb09f7a35def4e008faf3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="icommand-ole-db"></a>ICommand(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server에만 적용 되는 OLE DB 동작에 설명 합니다.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 열 크기보다 큰 데이터를 삽입하면 일반적으로 오류가 발생합니다. 그러나 경우에 따라서는 S_OK가 반환되는 상황에서 *dwStatus* 가 DBSTATUS_S_TRUNCATED로 설정될 수도 있습니다. 일반적으로 발생 매개 변수를 사용 하 여 데이터를 삽입할 때 여기서 열 데이터를 보관 하기에 충분 하지 않으면 및 **icommandwithparameters:: Setparameterinfo** 호출 되지 않았습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [인터페이스 & #40; OLE db& #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
