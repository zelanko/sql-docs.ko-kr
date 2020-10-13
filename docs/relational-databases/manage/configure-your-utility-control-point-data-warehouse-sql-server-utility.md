---
title: 유틸리티 제어 지점 데이터 웨어하우스 구성(SQL Server 유틸리티) | Microsoft 문서
description: SQL Server 인스턴스가 데이터를 저장하는 유틸리티 관리 데이터 웨어하우스에 대해 알아봅니다. 데이터 보존 기간 및 디렉터리를 구성하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 06080937156afc4e38c9ef59bd9b92e98695eb57
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867872"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>유틸리티 제어 지점 데이터 웨어하우스 구성(SQL Server 유틸리티)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 수집된 데이터는 UMDW(유틸리티 관리 데이터 웨어하우스)에 저장됩니다. UMDW의 파일 이름은 sysutility_mdw입니다.  
  
 UMDW 데이터 보존 기간을 구성할 수 있습니다. 자세한 내용은 [유틸리티 관리&#40;SQL Server 유틸리티&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))를 참조하세요.  
  
 다음 구성 설정은 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스에서 구성할 수 없습니다.  
  
-   UMDW 이름: Sysutility_mdw  
  
-   컬렉션 집합 업로드 빈도: 15분마다  
  
 UMDW 디렉터리는 구성할 수 있으며 \<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\입니다. 여기서 \<System drive>는 일반적으로 C:\ 드라이브입니다. 로그 파일 Sysutility_mdw_\<GUID>_LOG는 같은 디렉터리에 있습니다.  
  
> [!NOTE]  
>  UMDW(sysutility_mdw) 파일 위치는 detach/attach 또는 ALTER DATABASE를 사용하여 변경할 수 있으며 ALTER DATABASE를 사용하는 것이 좋습니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
