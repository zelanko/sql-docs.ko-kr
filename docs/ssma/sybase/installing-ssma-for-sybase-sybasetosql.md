---
title: SAP ASE 용 SSMA 설치 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 91a4dfcf8add3900c51e33a6e40fa874ce9f9798
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028967"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>SAP ASE 용 SSMA 설치 (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP 적응 서버 Enterprise (ASE) 용 SSMA (Migration Assistant)는 SAP ASE에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database로의 마이그레이션을 수행 하는 데 사용 하는 클라이언트 응용 프로그램으로 구성 됩니다. 또한 마이그레이션된 데이터베이스에서 데이터 마이그레이션을 지 원하는 확장 팩과 ASE 시스템 함수를 사용할 수 있습니다.  
  
마이그레이션 단계를 수행 하려는 컴퓨터에 클라이언트 응용 프로그램을 설치 합니다. 마이그레이션된 데이터베이스를 호스팅할를 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 컴퓨터에 확장 팩 파일을 설치 합니다.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>SAP ASE 용 SSMA 업그레이드  
SAP ASE 용 SSMA의 이후 버전으로 업그레이드 하려면 먼저 클라이언트와 서버 확장 팩을 제거 해야 합니다. 그런 다음 최신 버전을 설치 합니다.  
  
이전 버전의 SAP ASE 용 SSMA에서 프로젝트를 여는 경우 SSMA는 프로젝트를 최신 버전으로 변환할지 여부를 묻는 메시지를 표시 합니다. 최신 버전의 SSMA에서 프로젝트를 사용 하려면 **예** 를 클릭 합니다.  
  
## <a name="contents"></a>콘텐츠  
  
|아티클|설명|  
|---------|---------------|  
|[SAP ASE 용 SSMA 클라이언트 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|SAP ASE 클라이언트용 SSMA를 설치 하기 위한 정보와 지침을 제공 합니다.|  
|[SQL Server &#40;SybaseToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|인스턴스에 확장 팩을 설치 하는 방법에 대 한 정보와 지침 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 제공 합니다.|  
|[SybaseToSQL&#41;&#40;SAP ASE 구성 요소에 대 한 SSMA 제거](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|클라이언트 프로그램 및 확장 팩을 제거 하는 방법에 대 한 지침을 제공 합니다.|  
  
## <a name="see-also"></a>참고 항목  
[SAP ASE 데이터베이스를 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;로 마이그레이션](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
