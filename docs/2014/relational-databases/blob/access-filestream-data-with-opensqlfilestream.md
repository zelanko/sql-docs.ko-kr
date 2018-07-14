---
title: OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: filestream
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- OpenSqlFilestream
api_location:
- sqlncli11.dll
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ee7c3745466565a5baf8262fe6cc20dc80c0a3d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250343"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스
  OpenSqlFilestream API는 FILESTREAM binary large object (BLOB) 파일 시스템에 저장 된에 대 한 Win32 호환 파일 핸들을 가져옵니다. 핸들이 [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)또는 [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427)의 Win32 API 중 하나로 전달될 수 있습니다. 이 핸들을 다른 Win32 API에 전달하면 ERROR_ACCESS_DENIED 오류가 반환됩니다. 핸들은 트랜잭션이 커밋 또는 롤백되기 전에 Win32 [CloseHandle](http://go.microsoft.com/fwlink/?LinkId=86428) API에 전달하는 방식으로 닫아야 합니다. 핸들을 닫지 못하면 서버 쪽 리소스 노출이 발생합니다.  
  
 모든 FILESTREAM 데이터 컨테이너 액세스에서 수행 해야 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문도 동일한 트랜잭션에서 실행할 수 있습니다. 이를 통해 SQL 데이터와 FILESTREAM BLOB 데이터 간의 일관성을 유지 관리할 수 있습니다.  
  
 Win32를 사용하여 FILESTREAM BLOB에 액세스하려면 [Windows 인증](../security/choose-an-authentication-mode.md) 을 설정해야 합니다.  
  
> [!IMPORTANT]  
>  파일이 쓰기 액세스 권한으로 열린 경우 트랜잭션은 FILESTREAM 에이전트의 소유입니다. 트랜잭션이 해제되기 전까지는 Win32 파일 I/O만 허용됩니다. 트랜잭션을 해제하려면 쓰기 핸들을 닫아야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
  HANDLE OpenSqlFilestream (  
  LPCWSTR  
  FilestreamPath  
  ,  
  SQL_FILESTREAM_DESIRED_ACCESS  
  DesiredAccess,  
ULONGOpenOptions,LPBYTEFilestreamTransactionContext,SIZE_TFilestreamTransactionContextLength,PLARGE_INTEGERAllocationSize);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *FilestreamPath*  
 [in] `nvarchar(max)` 에서 반환 되는 경로 [PathName](/sql/relational-databases/system-functions/pathname-transact-sql) 함수입니다. PathName은 FILESTREAM 테이블 및 열에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT 또는 UPDATE 권한이 있는 계정의 컨텍스트에서 호출해야 합니다.  
  
 *DesiredAccess*  
 [in] FILESTREAM BLOB 데이터에 액세스하는 데 사용되는 모드를 설정합니다. 이 값은 [DeviceIoControl Function](http://go.microsoft.com/fwlink/?LinkId=105527)(DeviceIoControl 함수)에 전달됩니다.  
  
|속성|값|의미|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|데이터를 파일에서 읽을 수 있습니다.|  
|SQL_FILESTREAM_WRITE|1|데이터를 파일에 쓸 수 있습니다.|  
|SQL_FILESTREAM_READWRITE|2|데이터를 파일에서 읽고 쓸 수 있습니다.|  
  
> [!NOTE]  
>  이러한 값은 sqlncli.h의 SQL_FILESTREAM_DESIRED_ACCESS 열거에서 정의합니다.  
  
 *OpenOptions*  
 [in] 파일 특성 및 플래그입니다. 이 매개 변수는 다음 플래그의 조합을 포함할 수도 있습니다.  
  
|플래그|값|의미|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|특별한 옵션 없이 파일을 열거나 만듭니다.|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|비동기 I/O를 위해 파일을 열거나 만듭니다.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|시스템에서 시스템 캐싱을 사용하지 않고 파일을 엽니다.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|시스템에서 중간 캐시를 통해 쓰지 않습니다. 쓰기는 디스크에 바로 적용됩니다.|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|처음부터 끝까지 순차적으로 파일에 액세스합니다. 시스템에서는 이 필드를 힌트로 사용하여 파일 캐싱을 최적화할 수 있습니다. 응용 프로그램에서 임의 액세스를 위해 파일 포인터를 이동하는 경우 최적 캐싱이 수행되지 않을 수도 있습니다.|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|파일에 임의로 액세스합니다. 시스템에서는 이 필드를 힌트로 사용하여 파일 캐싱을 최적화할 수 있습니다.|  
  
 *FilestreamTransactionContext*  
 [in] [GET_FILESTREAM_TRANSACTION_CONTEXT](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) 함수에서 반환하는 값입니다.  
  
 *FilestreamTransactionContextLength*  
 [in] 바이트 수를 `varbinary(max)` GET_FILESTREAM_TRANSACTION_CONTEXT 함수에서 반환 되는 데이터입니다. 이 함수는 N바이트의 배열을 반환합니다. N은 함수에 의해 결정되며, 반환되는 바이트 배열의 속성입니다.  
  
 *AllocationSize*  
 [in] 데이터 파일의 처음 할당 크기(바이트)를 지정합니다. 읽기 모드에서는 무시됩니다. 이 매개 변수는 NULL일 수 있으며, 이 경우 기본 파일 시스템 동작이 사용됩니다.  
  
## <a name="return-value"></a>반환 값  
 이 함수가 성공적으로 실행되면 지정된 파일에 대해 열린 핸들이 반환되고 함수가 실패하면 INVALID_HANDLE_VALUE가 반환됩니다. 확장 오류 정보를 보려면 GetLastError()를 호출합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `OpenSqlFilestream` API를 사용하여 Win32 핸들을 가져오는 방법을 보여 줍니다.  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
## <a name="remarks"></a>Remarks  
 이 API를 사용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 설치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 도구와 함께 설치됩니다. 자세한 내용은 [Installing SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md)(SQL Server Native Client 설치)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Binary Large Object &#40;Blob&#41; 데이터 &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)   
 [FILESTREAM 데이터 부분 업데이트](make-partial-updates-to-filestream-data.md)   
 [FILESTREAM 응용 프로그램에서 데이터베이스 작업과의 충돌 방지](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
