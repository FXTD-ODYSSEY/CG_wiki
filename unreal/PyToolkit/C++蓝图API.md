
# C++ 蓝图 API

> &emsp;&emsp;我这里整合了 Youtube Unreal Python 教程的 C++ 代码 [视频](https://www.youtube.com/watch?v=RwWgC2xqk48) [github](https://github.com/AlexQuevillon/UnrealPythonLibrary)    
> &emsp;&emsp;并对他的代码进行了升级迭代。

# UnrealPythonLibrary

## GetAllProperties

    Python -> unreal.PyToolkitBPLibrary.get_all_properties
    ---
    Param
      UClass          = Python 传递 class 类型
    Return
      TArray<FString> = 返回类型内置的 property 属性

> &emsp;&emsp;用来获取类型的 property 省得查源码或者看文档。

## SetSelectedAssets

    Python -> unreal.PyToolkitBPLibrary.set_selected_assets
    ---
    Param
      TArray<FString> = 设置选择文件的路径

## GetSelectedFolders

    Python -> unreal.PyToolkitBPLibrary.get_selected_folders
    ---
    Return
      TArray<FString> = 返回当前选择的文件夹路径

## SetSelectedFolders

    Python -> unreal.PyToolkitBPLibrary.set_selected_folders
    ---
    Param
      TArray<FString> = 设置选择文件夹的路径

## CloseEditorForAssets

    Python -> unreal.PyToolkitBPLibrary.close_editor_for_assets
    ---
    Param
      TArray<UObject *> = 根据传递的资源关闭编辑器

## GetAssetsOpenedInEditor

    Python -> unreal.PyToolkitBPLibrary.get_assets_opened_in_editor
    ---
    Return
      TArray<UObject *> = 获取当前打开的 asset 

## SetFolderColor

    Python -> unreal.PyToolkitBPLibrary.set_folder_color
    ---
    Param
      FString      = 文件夹路径
      FLinearColor = 颜色

## GetActiveViewportIndex

    Python -> unreal.PyToolkitBPLibrary.get_active_viewport_index
    ---
    Return
      int      = 返回当前 Viewport 的序号

## SetViewportLocationAndRotation

    Python -> unreal.PyToolkitBPLibrary.set_viewport_location_and_rotation
    ---
    Param
      int      = Viewport 编号
      FVector  = 设置位移
      FRotator = 设置旋转

# Sequencer API

## GetSequencerSequence

    Python -> unreal.PyToolkitBPLibrary.get_sequencer_sequence
    ---
    Return
      ULevelSequence = 当前打开的 LevelSequence

## GetSequencerSelectedID

    Python -> unreal.PyToolkitBPLibrary.get_sequencer_selected_id
    ---
    Return
      ULevelSequence = 获取 LevelSequence
    Return
      TArray<FGuid>  = 返回当前选择的 ID

## GetSequencerSelectedTracks

    Python -> unreal.PyToolkitBPLibrary.get_sequencer_selected_tracks
    ---
    Return
      ULevelSequence             = 获取 LevelSequence
    Return
      TArray<UMovieSceneTrack *> = 返回当前选择的 Track

## GetSequencerSelectedSections

    Python -> unreal.PyToolkitBPLibrary.get_sequencer_selected_sections
    ---
    Return
      ULevelSequence               = 获取 LevelSequence
    Return
      TArray<UMovieSceneSection *> = 返回当前选择的 Section

## GetSequencerSelectedChannels

    Python -> unreal.PyToolkitBPLibrary.get_sequencer_selected_channels
    ---
    Return
      ULevelSequence               = 获取 LevelSequence
    Return
      TMap<UMovieSceneSection *, FString> = 返回当前所选 Section 对应的 Channel 名称


# SocketAPI

## AddSkeletalMeshSocket

    Python -> unreal.PyToolkitBPLibrary.add_skeletal_mesh_socket
    ---
    Param:
      USkeleton  - 骨架对象
      FString    - 骨骼名称
    Return:
      USkeletalMeshSocket  - 返回生成的 SkeleMeshSocket 

## AddSkeletalMeshSocket

    Python -> unreal.PyToolkitBPLibrary.add_skeletal_mesh_socket
    ---
    Param:
      USkeleton  - 骨架对象
      FString    - 骨骼名称
    Return:
      USkeletalMeshSocket  - 返回生成的 SkeleMeshSocket 

## GetSkeletonBoneNum

    Python -> unreal.PyToolkitBPLibrary.get_skeleton_bone_num
    ---
    Param:
      USkeleton  - 骨架对象

## GetSkeletonBoneName

    Python -> unreal.PyToolkitBPLibrary.get_skeleton_bone_name
    ---
    Param:
      USkeleton  - 骨架对象
      int32      - 骨骼序号

# Msic API

## AddComponent

    Python -> unreal.PyToolkitBPLibrary.add_component
    ---
    Param:
      AActor           - Componet 添加的 Actor
      USceneComponent  - Componet 父对象
      FName            - Componet 名称
      UClass           - Componet 类型
    Return:
      UActorComponent  - 返回添加的 Component


## RenderTargetCubeCreateStaticTextureCube

    Python -> unreal.PyToolkitBPLibrary.render_target_cube_create_static_texture_cube
    ---
    Param:
      UTextureRenderTargetCube  - RenderTargetCube 对象
      FString                   - 输出名称
    Return:
      UTextureCube  - 返回生成的 Texture 

## GetCurrentContentPath

    Python -> unreal.PyToolkitBPLibrary.get_current_content_path
    ---
    Return
      FString = 当前 Content Browser 的路径