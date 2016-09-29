---
layout: post
category: "javascript"
title: "gulp 配置文件"
tags: ["javascript","gulp","自动化构建工具"]
---

整理近期使用过的 gulp 配置文件，包含了对整个项目的js压缩，less转css等。

```` javascript

var gulp        = require('gulp'),                  // gulp主文件
    less        = require('gulp-less'),             // less转css
    del         = require('del'),                   // 文件清除删除
    cleanCSS    = require('gulp-clean-css'),        // css压缩
    uglify      = require('gulp-uglify'),           // js压缩
    browserSync = require('browser-sync').create()  // 服务器-浏览器同步刷新服务

var DST_DIR     = './dist/'                       	// 发布文件所在文件夹

/**** clean ****/
gulp.task('clean',function(){
  return del(DST_DIR).then(function(paths){
    console.log('已删除：'+paths.join('\n'))
  })
})

/**** less转css压缩 ****/
gulp.task('less',function(){
  return gulp.src('./src/css/**/*.less')
             .pipe(less())
             .pipe(cleanCSS())
             .pipe(gulp.dest(DST_DIR+'src/css/'))
})

/**** js压缩 ****/
gulp.task('uglify',function(){
  return gulp.src('./src/js/**/*.js')
             .pipe(uglify())
             .pipe(gulp.dest(DST_DIR+'src/js/'))
})

/**** 移动HTML文件到dist ****/
gulp.task('moveHTML',function(){
  return gulp.src('./tpl/*.html')
             .pipe(gulp.dest(DST_DIR+'tpl/'))
})

/**** 创建server ****/
gulp.task('server',function(){
  browserSync.init({
    server:DST_DIR
  })
})

/**** watch ****/
gulp.task('auto',function(){
  gulp.watch('./src/css/**/*.less',['less'])
  gulp.watch('./src/js/**/*.js',['uglify'])
  gulp.watch('./tpl/*.html',['moveHTML'])
  gulp.watch(DST_DIR+'**').on('change', browserSync.reload)
})

/**** default默认任务，整个流程跑一遍并watch文件 ****/
gulp.task('default',['less','uglify','moveHTML','server','auto'])

````