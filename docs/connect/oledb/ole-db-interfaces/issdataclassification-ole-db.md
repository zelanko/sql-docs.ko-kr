---
title: ISSDataClassification | Microsoft Docs
description: ISSDataClassification 인터페이스
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSDataClassification
apitype: COM
helpviewer_keywords:
- ISSDataClassification interface
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 328110f81f993c66a9455324ff8ec830b329b41b
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506662"
---
# <a name="issdataclassification"></a>ISSDataClassification
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSDataClassification** 인터페이스는 SQL Server에서 수신한 활성 행 집합에 대한 민감도 분류 데이터를 검색하는 기능을 제공합니다.
  

## <a name="methods"></a>메서드

|메서드|설명|  
|------------|-----------------|  
|[ISSDataClassification::GetSensitivityClassification](../../oledb/ole-db-interfaces/issdataclassification-getsensitivityclassification-ole-db.md)|민감도 분류 정보를 포함하는 SENSITIVITYCLASSIFICATION 구조체에 대한 포인터를 반환합니다.|  

## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [행 집합](../ole-db-rowsets/rowsets.md)   
 [데이터 분류 사용](../features/using-data-classification.md)
