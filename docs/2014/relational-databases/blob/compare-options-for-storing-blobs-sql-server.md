---
title: BLOB 저장 옵션 비교(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d682257669753665ac397133fcdec0f52e46dedd
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010345"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>BLOB 저장 옵션 비교(SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 파일 및 문서를 저장하는 데 사용할 수 있는 옵션을 설명하고 비교합니다.  
  
##  <a name="Expectations"></a> 데이터베이스에 파일 저장 - 이점 및 요구 사항  
 대부분의 기업 데이터는 본질적으로 구조화되어 있지 않으며 대개 파일 시스템에 파일 및 문서로 저장됩니다. 이러한 데이터는 대부분 Windows API를 통해 파일에 액세스하는 애플리케이션에서 생성, 관리 및 사용합니다. 일반적으로 기업에서는 이러한 데이터를 파일 시스템에 보관하는 한편, 파일의 관련 메타데이터는 관계형 데이터베이스에 저장합니다.  
  
 구조화되지 않은 데이터를 관계형 데이터베이스에 통합하면 상당한 이점을 얻을 수 있습니다. 이러한 이점은 다음과 같습니다.  
  
-   백업과 같은 통합된 스토리지 및 데이터 관리 기능을 이용할 수 있습니다.  
  
-   데이터 및 메타데이터에 대한 전체 텍스트 검색과 의미 체계 검색 같은 통합된 서비스를 이용할 수 있습니다.  
  
-   구조화되지 않은 데이터에 대한 관리 및 정책 관리가 용이해집니다.  
  
 대부분의 경우 구조화되지 않은 데이터는 관계형 데이터베이스에 저장할 수 없었습니다. 이전에는 관계형 시스템 상에서 기존의 Windows 기반 애플리케이션을 실행할 수 없었습니다. 또한 Microsoft Word 또는 Adobe Reader 같은 상용화된 애플리케이션을 관계형 데이터베이스 API 상에서 실행할 수 있도록 다시 작성하는 것은 실용적이지 않습니다. 이러한 애플리케이션에서는 단순히 Windows API를 통해 데이터에 액세스할 수 있기만 하면 됩니다. 즉, 다음과 같은 요구 사항을 충족해야 합니다.  
  
-   Windows 애플리케이션에서는 데이터베이스 트랜잭션을 인식하지 않으며 그럴 필요도 없습니다.  
  
-   Windows 애플리케이션에서는 파일 및 디렉터리 데이터에 대한 파일 시스템 API와의 호환성이 필요합니다.  
  
##  <a name="Filestream"></a> FILESTREAM  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 이미 파일 시스템에 파일로 저장된 구조화되지 않은 데이터를 효율적으로 저장, 관리 및 스트리밍할 수 있는 FILESTREAM 기능이 있습니다. 그러나 FILESTREAM 솔루션은 사용자 지정 프로그래밍이 필요하며, 위에서 설명한 Windows 애플리케이션 호환성에 대한 요구 사항을 충족하지 않습니다.  
  
##  <a name="FileTables"></a> FileTable  
 기존의 FILESTREAM 기능을 기반으로 구축된 FileTable 기능은 파일 기반 데이터에 대한 비트랜잭션 액세스 및 Windows 애플리케이션 호환성 요구 사항을 해결함으로써 기업 고객이 구조화되지 않은 파일 데이터 및 디렉터리 계층 구조를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장할 수 있게 해 줍니다.  
  
##  <a name="CompareFileTable"></a> FILESTREAM 및 FileTable 비교  
  
|기능|파일 서버 및 데이터베이스 솔루션|FILESTREAM 솔루션|FileTable 솔루션|  
|-------------|---------------------------------------|-------------------------|------------------------|  
|**단일화된 관리 태스크**|아니요|사용자 계정 컨트롤|**예**|  
|**단일 서비스 집합**: 검색, 보고, 쿼리 등|아니요|사용자 계정 컨트롤|**예**|  
|**통합 보안 모델**|아니요|사용자 계정 컨트롤|**예**|  
|**FILESTREAM 데이터의 현재 위치 업데이트**|사용자 계정 컨트롤|아니요|**예**|  
|**파일 및 디렉터리 계층 구조를 데이터베이스에서 유지 관리**|아니요|아니요|**예**|  
|**Windows 응용 프로그램 호환성**|사용자 계정 컨트롤|아니요|**예**|  
|**파일 특성에 대한 관계형 액세스**|아니요|아니요|**예**|  
  
##  <a name="CompareRBS"></a> FILESTREAM 및 RBS(Remote BLOB Store) 비교  
 이러한 두 기능에 대한 비교 내용은 RBS 팀의 블로그 게시물 [SQL Server Remote BLOB Store 및 FILESTREAM 기능 비교](https://go.microsoft.com/fwlink/?LinkId=210317)합니다.  
  
##  <a name="more"></a> 자세한 정보  
 [FILESTREAM&#40;SQL Server&#41;](filestream-sql-server.md)  
 [FileTables&#40;SQL Server&#41;](filetables-sql-server.md)  
 [RBS&#40;Remote Blob Store&#41;&#40;SQL Server&#41;](remote-blob-store-rbs-sql-server.md)  
  
