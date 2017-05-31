---
title: "BLOB(Binary Large Object) 데이터(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4a9291aa99091d1b44e4b829af803637250bd333
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="binary-large-object-blob-data-sql-server"></a>BLOB(Binary Large Object) 데이터(SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하면 데이터베이스 또는 원격 저장 장치에 파일 및 문서를 저장할 수 있습니다.  
  
##  <a name="section"></a> 섹션 내용  
 [BLOB 저장 옵션 비교&#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md)  
 FILESTREAM, FileTable 및 Remote Blob Store의 장점을 비교합니다.  
  
 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
 FILESTREAM을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기반 응용 프로그램에서 문서 및 이미지와 같은 구조화되지 않은 데이터를 파일 시스템에 저장할 수 있습니다. 응용 프로그램은 풍부한 스트리밍 API 및 파일 시스템의 성능을 활용할 수 있고 동시에 구조화되지 않은 데이터와 해당되는 구조화된 데이터 간에 트랜잭션 일관성을 유지할 수 있습니다.  
  
 [FileTables&#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
 FileTable 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 파일 데이터에 대해 Windows 파일 네임스페이스 및 Windows 응용 프로그램과의 호환성을 지원합니다. FileTable을 통해 응용 프로그램이 해당 저장소 및 데이터 관리 구성 요소를 통합할 수 있으며, 구조화되지 않은 데이터 및 메타데이터에 대한 통합 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스(전체 텍스트 검색 및 의미 체계 검색 포함)가 제공됩니다.  
  
 즉, 파일 및 문서를 FileTable이라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 특수 테이블에 저장할 수 있지만, Windows 응용 프로그램에서 해당 파일 및 문서에 액세스할 때는 파일 시스템에 저장된 파일 및 문서에 액세스할 때와 같은 방식으로 처리됩니다. 클라이언트 응용 프로그램을 변경할 필요는 없습니다.  
  
 [RBS&#40;Remote Blob Store&#41;&#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
 데이터베이스 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 RBS(Remote BLOB Store)를 사용하여 BLOB(Binary Large Object)를 서버에 직접 저장하지 않고 상용 저장소 솔루션에 저장할 수 있습니다. 이렇게 하면 용량을 크게 절약할 수 있고 고가의 서버 하드웨어 리소스 낭비를 방지할 수 있습니다. RBS는 응용 프로그램이 BLOB 데이터에 액세스하기 위한 표준화된 모델을 정의하는 API 라이브러리 집합을 제공합니다. RBS는 원격 BLOB 데이터 관리를 돕기 위해 가비지 수집 등의 유지 관리 도구도 제공합니다.  
  
 RBS는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어에 포함되어 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 의해 설치되지 않습니다.  
  
  
