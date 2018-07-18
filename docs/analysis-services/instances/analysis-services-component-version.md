---
title: SQL Server Analysis Services 누적 업데이트 빌드 버전 확인 | Microsoft Docs
ms.date: 07/11/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1da8384bb51360178e1735d13f6c6b706e8b7ff
ms.sourcegitcommit: 87efa581f7d4d84e9e5c05690ee1cb43bd4532dc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38999360"
---
# <a name="verify-analysis-services-cumulative-update-build-version"></a>Analysis Services 누적 업데이트 빌드 버전 확인

SQL Server 2017부터, Analysis Services 빌드 버전 번호 및 SQL Server 데이터베이스 엔진의 빌드 버전 번호가 일치 하지 않습니다. Analysis Services와 데이터베이스 엔진 모두에 동일한 설치 관리자를 사용 하는 동안 빌드 시스템은 각 사용 하 여 구분 됩니다.

 경우에 따라 CU (누적 업데이트) 빌드 패키지 적용 되었고 Analysis Services 구성 요소가 업데이트 된 경우를 확인 해야 할 수 있습니다. 특정 CU 용 빌드 버전 번호를 사용 하 여 컴퓨터에 설치 된 Analysis Services 구성 요소 파일의 빌드 버전 번호를 비교 하 여 확인할 수 있습니다.

## <a name="verify-component-file-version"></a>구성 요소 파일 버전을 확인

구성 요소 파일 버전을 확인 하려면 

1. 로 이동 [SQL Server 2017 빌드 버전](https://support.microsoft.com/help/4047329)합니다. 
2. **SQL Server 2017 누적 업데이트 (CU) 빌드**를 클릭 합니다 **기술 자료 번호** 확인 하려는 빌드에 대 한 합니다.
3. 에 **SQL Server 2017 누적 업데이트 (#)** 문서에 **누적 업데이트 패키지 정보** 섹션을 확장 하 고 **누적 업데이트 패키지 파일 정보**.
4. 에 **SQL Server 2017 Analysis Services** 테이블에 대 한 파일 버전을 확인 합니다 **msmdsrv.exe** 구성 요소 파일입니다. CU는 적용 된 경우 파일 버전 번호를 컴퓨터에 설치 된 msmdsrv.exe 파일을 일치 해야 합니다.

## <a name="see-also"></a>참고자료  

[SQL Server 서비스 업데이트 설치](../../database-engine/install-windows/install-sql-server-servicing-updates.md)  

[Microsoft SQL Server 용 업데이트 센터](https://msdn.microsoft.com/library/ff803383.aspx)
  
  
