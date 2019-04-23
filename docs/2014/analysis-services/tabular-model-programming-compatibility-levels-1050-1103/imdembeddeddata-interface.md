---
title: IMDEmbedded 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 9dba8c68-4bef-4c2b-815c-c286f1a1939b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 83e46e9b62359623093415ca456ecadd72f847cd
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155219"
---
# <a name="imdembedded-interface"></a>IMDEmbedded 인터페이스
  IMDEmbedded 인터페이스는 포함된 PowerPivot 데이터베이스 또는 테이블 형식 model 데이터베이스를 관리하는 데 사용되는 공용 인터페이스입니다. 이 인터페이스는 `IPersistStream` 인터페이스에서 상속됩니다. 이 인터페이스에서는 다음 작업이 허용됩니다.  
  
-   컨테이너 문서의 포함된 스트림에 대한 식별자를 가져옵니다.  
  
-   포함하는 문서의 URL을 설정합니다.  
  
-   포함하는 애플리케이션이 호스팅된 환경에 있는지 여부를 나타내는 플래그를 설정합니다.  
  
-   포함하는 애플리케이션에 사용되는 임시 파일에 대한 경로를 설정합니다.  
  
-   현재 포함된 작업을 취소합니다.  
  
-   포함된 개체를 저장하기 위해 스트림의 예상 크기(바이트)를 가져옵니다. `IPersistStream`에서 상속됩니다.  
  
-   포함된 데이터베이스가 마지막으로 저장된 후에 변경되었는지 여부를 확인합니다. `IPersistStream`에서 상속됩니다.  
  
-   포함된 데이터베이스를 로컬 또는 in-process 엔진에 로드합니다. `IPersistStream`에서 상속됩니다.  
  
-   로컬 또는 in-process 데이터베이스를 컨테이너 문서의 포함된 스트림에 저장합니다. `IPersistStream`에서 상속됩니다.  
  
## <a name="reference"></a>참조  
 다음 문서를 참조 합니다 `IMDEmbedded` 인터페이스에 제공 된 대로 **msmd.h** 헤더 파일입니다.  
  
### <a name="source-file-pxoembeddeddataidl"></a>소스 파일: PXOEmbeddedData.idl  
  
```  
[  
  local,                            
  object,                           
  uuid(6B6691CF-5453-41c2-ADD9-4F320B7FD421),                       
  pointer_default(unique)           
]  
interface IMDEmbeddedData : IPersistStream  
{  
 [id(1), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in] BOOL in_fIsHosted);  
  
 [id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
  
 [id(3), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
  
 [id(4), helpstring("Set the path used by the embedding application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
  
 [id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
};  
```  
  
### <a name="imdembeddeddatagetstreamidentifier"></a>IMDEmbeddedData::GetStreamIdentifier  
  
```  
HRESULT GetStreamIdentifier (  
    [out, retval] BSTR * out_pbstrStreamId  
    )  
```  
  
#### <a name="description"></a>Description  
 호스트 애플리케이션에 사용되는 식별자를 컨테이너 문서의 포함된 스트림에 가져옵니다.  
  
#### <a name="parameters"></a>매개 변수  
 *out_pbstrStreamId*  
 스트림 식별자의 위치를 지정합니다.  
  
#### <a name="return-value"></a>반환 값  
 `S_OK`  
 스트림 식별자가 반환되었습니다.  
  
 `S_FALSE`  
 스트림 식별자가 없습니다.  
  
 `E_FAIL`  
 스트림 식별자에 액세스하는 동안 오류가 발생했습니다.  
  
#### <a name="remarks"></a>Remarks  
 현재 연결에 포함된 데이터베이스가 포함되어 있는지 확인하려면 OLE DB 연결 속성에서 DBPROP_MSMD_EMBEDDED_DATA 속성 값을 확인해야 합니다.  
  
 DBPROP_MSMD_EMBEDDED_DATA의 가능한 값은 다음과 같습니다.  
  
|이름|값|정의|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|포함된 데이터베이스를 사용할 수 없습니다.|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|현재 애플리케이션에 포함된 데이터베이스가 포함되어 있습니다.|  
|DBPROPVAL_EMBED_LINKED|0x02|포함된 데이터베이스가 원격 애플리케이션(예: SharePoint Server)에서 호스팅됩니다.|  
  
#### <a name="source"></a>원본  
  
```  
[id(1), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
```  
  
### <a name="imdembeddeddatasetcontainerurl"></a>IMDEmbeddedData::SetContainerURL  
  
```  
HRESULT SetContainerURL (  
    [in] BSTR in_bstrURL  
    )  
```  
  
#### <a name="description"></a>Description  
 포함된 스트림을 포함하는 파일의 URL을 설정합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *in_bstrURL*  
 포함하는 문서의 URL을 지정합니다.  
  
#### <a name="return-value"></a>반환 값  
 `S_OK`  
 컨테이너 URL을 설정했습니다.  
  
 `E_FAIL`  
 컨테이너 URL을 설정하는 동안 오류가 발생했습니다.  
  
#### <a name="source"></a>원본  
  
```  
[id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
```  
  
### <a name="imdembeddeddatasethosted"></a>IMDEmbeddedData::SetHosted  
  
```  
HRESULT SetHosted (  
    [in] BOOL in_fIsHosted  
    )  
```  
  
#### <a name="description"></a>Description  
 포함하는 애플리케이션이 호스팅된 환경에 있는지 여부를 나타내는 플래그를 설정합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *in_ftHosted*  
 호출자가 서비스 애플리케이션(예: IIS)의 호스팅된 환경에 있으면 TRUE입니다.  
  
#### <a name="return-value"></a>반환 값  
 `S_OK`  
 플래그를 설정했습니다.  
  
 `E_FAIL`  
 플래그를 설정하는 동안 오류가 발생했습니다.  
  
#### <a name="source"></a>원본  
  
```  
[id(5), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in]  BOOL in_fIsHosted);  
```  
  
### <a name="imdembeddeddatasettempdirpath"></a>IMDEmbeddedData::SetTempDirPath  
  
```  
HRESULT SetTempDirPath (  
    [in] BSTR in_bstrPath  
    )  
```  
  
#### <a name="description"></a>Description  
 포함하는 애플리케이션에 사용되는 임시 파일에 대한 경로를 설정합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *in_bstrPath*  
 임시 파일에 대한 호스트 애플리케이션에서 사용하는 경로입니다.  
  
#### <a name="return-value"></a>반환 값  
 `S_OK`  
 임시 파일 디렉터리를 설정했습니다.  
  
 `E_FAIL`  
 경로를 설정하는 동안 오류가 발생했습니다.  
  
#### <a name="source"></a>원본  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>Description  
 현재 포함된 데이터베이스 작업을 취소합니다.  
  
#### <a name="parameters"></a>매개 변수  
 없음  
  
#### <a name="return-value"></a>반환 값  
 `S_OK`  
 작업을 취소했습니다.  
  
 `DB_E_CANTCANCEL`  
 취소할 수 없는 작업이 현재 진행 중입니다.  
  
 `E_FAIL`  
 포함된 작업을 취소하는 동안 오류가 발생했습니다.  
  
#### <a name="source"></a>원본  
  
```  
[id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
```  
  
### <a name="imdembeddeddatagetsizemax-ipersiststreamgetsizemax"></a>IMDEmbeddedData::GetSizeMax (IPersistStream::GetSizeMax)  
  
```  
HRESULT GetSizeMax (  
    [out] ULARGE_INTEGER * out_pcbSize  
    )  
```  
  
#### <a name="description"></a>Description  
 포함된 개체를 저장하기 위해 스트림의 예상 크기(바이트)를 가져옵니다. `IPersistStream`에서 상속됩니다.  
  
#### <a name="parameters"></a>매개 변수  
 *in_bstrPath*  
 포함된 데이터베이스 이미지의 예상 크기(바이트)입니다.  
  
#### <a name="return-value"></a>반환 값  
 `S_OK`  
 크기를 가져왔습니다.  
  
 `E_FAIL`  
 크기를 가져오는 동안 오류가 발생했습니다.  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>Description  
 포함된 데이터베이스가 마지막으로 저장된 후에 변경되었는지 여부를 확인합니다. `IPersistStream`에서 상속됩니다.  
  
#### <a name="parameters"></a>매개 변수  
 none  
  
#### <a name="return-values"></a>반환 값  
 `S_OK`  
 데이터베이스가 마지막으로 저장된 후에 변경되었습니다.  
  
 `S_FALSE`  
 데이터베이스가 마지막으로 저장된 후에 변경되지 않았습니다.  
  
 `E_FAIL`  
 데이터베이스 상태를 가져오는 동안 오류가 발생했습니다.  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>Description  
 포함된 데이터베이스를 로컬 또는 in-process 엔진에 로드합니다. `IPersistStream`에서 상속됩니다.  
  
#### <a name="parameters"></a>매개 변수  
 *in_pStm*  
 포함된 데이터베이스를 로드할 스트림 인터페이스에 대한 포인터입니다.  
  
#### <a name="return-values"></a>반환 값  
 `S_OK`  
 데이터베이스를 로드했습니다.  
  
 `E_OUTOFMEMORY`  
 메모리가 부족하여 데이터베이스를 로드할 수 없습니다.  
  
 `E_FAIL`  
 데이터베이스를 로드하는 동안 오류가 발생했습니다. `E_OUTOFMEMORY`와 다릅니다.  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>Description  
 로컬 또는 in-process 데이터베이스를 컨테이너 문서의 포함된 스트림에 저장합니다. `IPersistStream`에서 상속됩니다.  
  
#### <a name="parameters"></a>매개 변수  
 *in_pStm*  
 포함된 데이터베이스를 저장할 스트림 인터페이스에 대한 포인터입니다.  
  
 *in_fClearDirty*  
 이 작업 후에 변경 플래그를 지워야 하는지 여부를 나타내는 플래그입니다.  
  
#### <a name="return-values"></a>반환 값  
 `S_OK`  
 데이터베이스를 저장했습니다.  
  
 `STG_E_CANTSAVE`  
 데이터베이스를 저장하는 동안 오류가 발생했습니다. `STG_E_MEDIUMFULL`과 다릅니다.  
  
 `STG_E_MEDIUMFULL`  
 저장 디바이스에 남아 있는 공간이 없으므로 데이터베이스를 저장할 수 없습니다.  
  
  
