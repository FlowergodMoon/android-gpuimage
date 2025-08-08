cmake_minimum_required(VERSION 3.19)

project(GPUImage)

# 创建共享库 (目标名: yuv-decoder)
add_library(
        yuv-decoder  # 目标名称
        SHARED
        src/main/cpp/yuv-decoder.c  # 源文件
)

# 查找日志库
find_library(
        log-lib
        log
)

# ===== 关键修复 1：使用正确的目标名称 =====
target_link_options(yuv-decoder PRIVATE  # 目标名改为 yuv-decoder
        "LINKER:-z,max-page-size=16384"      # 16KB 对齐标志
)

# ===== 关键修复 2：添加必要的包含目录 =====
# 假设有头文件目录，添加以下行（根据实际路径调整）
# target_include_directories(yuv-decoder PRIVATE include)

# 链接库
target_link_libraries(
        yuv-decoder  # 目标名称

        # 链接的库
        ${log-lib}
        GLESv2
        jnigraphics
)