---
title: "분석 플랫폼 시스템 확장 데이터 웨어하우스의에서 새로운 기능"
author: happynicolle
ms.author: nicw;barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Microsoft® 분석 플랫폼 시스템, MPP SQL Server 병렬 데이터 웨어하우스를 호스팅하는 확장 온-프레미스 어플라이언스의에서 새로운 기능을 참조 하십시오."
ms.date: 11/28/2016
ms.topic: article
ms.openlocfilehash: 3dc1a338ced5aa90ada112b97c4a6f13777da409
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="whats-new-in-analytics-platform-system-2016-a-scale-out-mpp-data-warehouse"></a>확장 MPP 데이터 웨어하우스 분석 플랫폼 시스템 2016의 새로운 기능
새로운 기능에서 Microsoft® Analytics Platform System (APS) 2016 최신 어플라이언스 업데이트 MPP SQL Server 병렬 데이터 웨어하우스를 호스팅하는 확장 온-프레미스 어플라이언스에 대 한 참조입니다. 

## <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 최신 SQL Server 2016 버전에서 실행 하 고 기본 데이터베이스 호환성 수준 130을 사용 합니다.  SQL Server 2016을 사용 하면 PolyBase에 대 한 클러스터형된 columnstore 인덱스 및 Kerberos에 대 한 지원 보조 인덱스와 같은 새로운 기능 중 일부를 수 있습니다. 


## <a name="t-sql"></a>T-SQL
APS 2016 T-SQL 호환성 향상 된 기능을 지원합니다.  이러한 추가 언어 요소 쉽게에서 SQL Server 및 기타 데이터 소스를 마이그레이션합니다. 

- [SQL 데이터 정렬은 열 수준][] Windows 데이터 정렬 이외에 이제 지원 됩니다.
- [클러스터형된 columnstore 인덱스의 비클러스터형 인덱스][] 클러스터형된 columnstore 인덱스에 있는 특정 값을 검색 하는 쿼리의 성능을 개선 합니다. 
- [선택... 에][] 
- [sp_spaceused()][] 디스크 공간 사용 또는 테이블이 나 데이터베이스에서 예약 된이 표시 됩니다.
- [넓은 테이블][] 지원은 SQL Server 2016으로 동일 합니다. 행 크기에 대 한 이전 제한인 32 K 더 이상 없습니다. 

### <a name="data-types"></a>데이터 형식

- [Varchar (max)][], [nvarchar (max)][] 및 [varbinary (max)][]합니다. 이러한 LOB 데이터 형식이 있는 최대 크기는 2GB입니다. 로드 하는 이러한 개체가 사용 [bcp 유틸리티][]합니다. Polybase 및 dwloader 지원 하지 않습니다 현재 이러한 데이터 형식입니다. 
- [SYSNAME][]
- [고유 식별자][]
- [숫자][] 및 DECIMAL 데이터 형식입니다.

### <a name="window-functions"></a>창 함수

- [ROWS 또는 RANGE][] SELECT 문의 OVER 절에 있습니다.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

### <a name="security-functions"></a>보안 함수

- [CHECKSUM()][] 및 [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

### <a name="additional-functions"></a>추가 기능

- [NEWID)][]
- [RAND)][]

## <a name="polybasehadoop-enhancements"></a>PolyBase Hadoop/향상 된 기능

- Hortonworks HDP 2.4 및 HDP 2.5와의 호환성
- 데이터베이스 범위 자격 증명을 통해 Kerberos 지원
- Azure 저장소 Blob을 사용한 자격 증명 지원

## <a name="install-and-upgrade-enhancements"></a>설치 및 업그레이드의 향상 된 기능

### <a name="enterprise-architecture-updates"></a>엔터프라이즈 아키텍처 업데이트
APS 2016으로 업그레이드 하는 기존 어플라이언스 최신 펌웨어 및 보안 픽스를 포함 하는 드라이버 업데이트를 설치 합니다. 

새로운 어플라이언스 HPE 또는 DELL에서 최신 업데이트를 모두 포함 및:

- 최신 세대 프로세서 지원 (Broadwell)
- DDR4 Dimm를 업데이트 합니다.
- DIMM 처리량 향상된

### <a name="integration"></a>통합

- 완전히 정규화 된 도메인 이름 (FQDN) 지원을 통해 기기에 도메인 트러스트를 설정할 수 있습니다. 
- FQDN을 사용 하려면 전체 업그레이드를 수행 하 고 업그레이드 하는 동안 옵트인 해야 합니다. 

### <a name="reduced-downtime"></a>가동 중지 시간 감소
APS 2016으로 업그레이드 하거나 설치는 빠르고 이전 버전 보다 덜 가동 중지 시간이 필요 합니다. 설치 또는 업그레이드, 가동 중지 시간을 줄입니다. 

 - 2016 년 6 월을 통해 업데이트를 모두 포함 된 이미지를 사용 하 여 WSUS 업데이트를 적용 하는 간소화
 - 드라이버 및 펌웨어 업데이트와 보안 업데이트 적용
 - 다운로드 하려면 필요 없이 설치할 수 있도록 어플라이언스 최신 핫픽스 및 어플라이언스 확인 유틸리티 (PAV)를 배치 합니다.


<!--MSDN references-->
[database compatibility level 130]:https://msdn.microsoft.com/library/bb510680.aspx
[SQL 데이터 정렬은 열 수준]:https://msdn.microsoft.com/library/ms143726.aspx
[클러스터형된 columnstore 인덱스의 비클러스터형 인덱스]:https://msdn.microsoft.com/library/ms188783.aspx
[Varchar (max)]:https://msdn.microsoft.com/library/ms176089.aspx
[nvarchar (max)]:https://msdn.microsoft.com/library/ms186939.aspx
[varbinary (max)]:https://msdn.microsoft.com/library/ms188362.aspx
[SYSNAME]:https://msdn.microsoft.com/library/ms188021.aspx
[선택... 에]:https://msdn.microsoft.com/library/ms188029.aspx
[sp_spaceused()]:https://msdn.microsoft.com/library/ms188776.aspx
[넓은 테이블]:https://msdn.microsoft.com/library/ms143432.aspx
[BULK INSERT]:https://msdn.microsoft.com/library/ms188365.aspx
[bcp 유틸리티]:https://msdn.microsoft.com/library/ms162802.aspx
[고유 식별자]:https://msdn.microsoft.com/library/ms187942.aspx
[숫자]:https://msdn.microsoft.com/library/ms187746.aspx
[ROWS 또는 RANGE]:https://msdn.microsoft.com/library/ms189461.aspx
[FIRST_VALUE]:https://msdn.microsoft.com/library/hh213018.aspx
[LAST_VALUE]:https://msdn.microsoft.com/library/hh231517.aspx
[CUME_DIST]:https://msdn.microsoft.com//library/hh231078.aspx
[PERCENT_RANK]:https://msdn.microsoft.com/library/hh213573.aspx
[CHECKSUM()]:https://msdn.microsoft.com/library/ms189788.aspx
[BINARY_CHECKSUM()]:https://msdn.microsoft.com/library/ms173784.aspx
[HAS_PERMS_BY_NAME()]:https://msdn.microsoft.com/library/ms189802.aspx
[NEWID)]:https://msdn.microsoft.com/library/ms190348.aspx
[RAND)]:https://msdn.microsoft.com/library/ms177610.aspx


  

  


