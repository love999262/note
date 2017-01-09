+ 确保安装了nodeJs，编辑器最好用webstorm，如果没有就用submileText

+  
```
npm install gulp -g   (global环境)
npm install gulp --save-dev (项目环境)
```
在全局环境以及项目环境下确保安装了gulp

+ 
在项目的根目录下建立gulpfile.js文件，里面的测试代码如下：
```
var gulp = require('gulp');

gulp.task('default', function() {
    // 将你的默认的任务代码放在这
    console.log("step1 finished");
});
```
CD到项目根目录下运行gulp命令测试，如果输出console.log里面的内容就表示第一步成功了。
+ 
在项目根目录下npm install 需要用到的模块，比如：
```
npm install gulp --save-dev gulp-imagemin
```
+ 
```

var gulp = require('gulp');
var less = require('gulp-less');
var rename = require('gulp-rename');
var uglify = require('gulp-uglify');
var minCss = require('gulp-minify-css');
var imageMin = require('gulp-imagemin');
gulp.task('html', function() {
    return gulp.src('src/*.html').
    pipe(gulp.dest('dist/'));
});

gulp.task('rename', function() {
    return gulp.src('src/js/*.js')
        .pipe(rename({ suffix: '.min' }))
        .pipe(gulp.dest('dist/js/'));
});

gulp.task('less', function() {
    return gulp.src('src/css/*.less')
        .pipe(less())
        .pipe(minCss())
        .pipe(gulp.dest('dist/css/'));
});

gulp.task('imageMin', function() {
    return gulp.src('src/images/*')
        .pipe(imageMin())
        .pipe(gulp.dest('dist/images/'))
});

gulp.task('watch', function() {
    gulp.watch('src/css/*', ['less']);
    gulp.watch('src/images/*', ['imageMin']);
    gulp.watch('src/*.html', ['html'])
});

gulp.task('default', ['less', 'rename', 'imageMin', 'html', 'watch']);


```
上面这段代码是最基本的gulp任务和watch应用，不做详细讲解，自己看。


 附录
var gulp = require('gulp'),
　　//代替 minifycss
　　cleanCSS = require('gulp-clean-css'),
　　//minifycss = require('gulp-minify-css'),
    concat = require('gulp-concat'),
    uglify = require('gulp-uglify'),
    rename = require('gulp-rename'),
    jshint=require('gulp-jshint');

    //语法检查
    gulp.task('jshint', function () {
        return gulp.src('js/*.js')
            .pipe(jshint())
            .pipe(jshint.reporter('default'));
    });

    //压缩css
    gulp.task('minifycss', function() {
        return gulp.src('css/*.css')    //需要操作的文件
            .pipe(rename({suffix: '.min'}))   //rename压缩后的文件名
            .pipe(cleanCSS({compatibility: 'ie7'}))   //执行压缩
            .pipe(gulp.dest('Css'));   //输出文件夹
    });

    //压缩,合并 js
    gulp.task('minifyjs', function() {
        return gulp.src('js/*.js')      //需要操作的文件
            .pipe(concat('main.js'))    //合并所有js到main.js
            .pipe(gulp.dest('js'))       //输出到文件夹
            .pipe(rename({suffix: '.min'}))   //rename压缩后的文件名
            .pipe(uglify())    //压缩
            .pipe(gulp.dest('Js'));  //输出
    });

　　//默认命令，在cmd中输入gulp后，执行的就是这个任务(压缩js需要在检查js之后操作)
    gulp.task('default',['jshint'],function() {
        gulp.start('minifycss','minifyjs'); 
　　});
