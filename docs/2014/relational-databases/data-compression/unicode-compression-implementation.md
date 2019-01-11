---
title: 유니코드 압축 구현 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a43a437b277c0fcc090a4ebd52d9deb14bec9fd0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756025"
---
# <a name="unicode-compression-implementation"></a>유니코드 압축 구현
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 SCSU(Standard Compression Scheme for Unicode) 알고리즘 구현을 사용하여 행 또는 페이지 압축 개체에 저장된 유니코드 값을 압축합니다. 이러한 압축 개체의 경우 `nchar(n)` 및 `nvarchar(n)` 열에 유니코드 압축이 자동으로 설정됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 로캘에 관계없이 유니코드 데이터가 2바이트로 저장됩니다. 이 방식을 UCS-2 인코딩이라고 합니다. 일부 로캘의 경우 SQL Server에서 SCSU 압축을 구현하면 스토리지 공간을 최대 50% 절약할 수 있습니다.  
  
## <a name="supported-data-types"></a>지원되는 데이터 형식  
 유니코드 압축은 고정 길이의 `nchar(n)` 및 `nvarchar(n)` 데이터 형식을 지원합니다. 행 외부 또는 `nvarchar(max)` 열에 저장된 데이터 값은 압축되지 않습니다.  
  
> [!NOTE]  
>  `nvarchar(max)` 데이터는 행에 저장되어 있더라도 유니코드 압축이 지원되지 않습니다. 하지만 이 데이터 형식에서 페이지 압축을 활용할 수 있습니다.  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>이전 버전의 SQL Server에서 업그레이드  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드되는 경우 유니코드 압축과 관련된 변경 내용은 압축 여부에 관계 없이 모든 데이터베이스 개체에 적용되지 않습니다. 데이터베이스가 업그레이드되면 개체는 다음과 같이 영향을 받습니다.  
  
-   압축되지 않은 개체의 경우 변경 내용이 적용되지 않고 이전과 같은 방식으로 계속 동작합니다.  
  
-   행 또는 페이지 압축 개체는 이전과 같은 방식으로 계속 동작하고 압축되지 않은 데이터는 값이 업데이트될 때까지 압축되지 않은 형식으로 유지됩니다.  
  
-   행 또는 페이지 압축 테이블에 삽입된 새 행은 유니코드 압축을 사용하여 압축됩니다.  
  
    > [!NOTE]  
    >  유니코드 압축의 장점을 모두 활용하려면 페이지 또는 행 압축을 사용하여 개체를 다시 작성해야 합니다.  
  
## <a name="how-unicode-compression-affects-data-storage"></a>유니코드 압축이 데이터 스토리지에 주는 영향  
 인덱스를 만들거나 다시 작성하는 경우 또는 행/페이지 압축을 사용하여 압축된 테이블에서 값을 변경하는 경우 영향을 받는 인덱스나 값은 압축된 크기가 현재 크기보다 작은 경우에만 압축 형식으로 저장됩니다. 이렇게 되면 유니코드 압축 때문에 테이블의 행 또는 인덱스의 크기가 증가하지 않습니다.  
  
 압축을 통해 절약할 수 있는 스토리지 공간은 압축하고 있는 데이터의 특성과 데이터 로캘에 따라 다릅니다. 다음 표에서는 로캘별로 절약할 수 있는 저장 공간을 보여 줍니다.  
  
|로캘|압축률|  
|------------|-------------------------|  
|영어|50%|  
|독일어|50%|  
|힌디어|50%|  
|터키어|48%|  
|베트남어|39%|  
|일본어|15%|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 압축](data-compression.md)   
 [sp_estimate_data_compression_savings&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql)   
 [페이지 압축 구현](page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql)  
  
  
