# Gulp接触笔记

> (名词解释: (pipe)用管道输送; (buffer)缓冲; (stream)流; (glob)匹配模式 )

## gulp.src(globs [, options])

**Zum Beispiel:**
```
gulp.src('client/js/**/*.js', { base: 'client' })
  .pipe(jade())
  .pipe(minify())
  .pipe(gulp.dest('build/minified_templates'));
```
  
例如匹配到其中一个文件, 路径为: 'client/js/bier/schwarzebier.js'
  
  * gulp.src接口的glob值为要匹配的文件路径, 本例中glob值为'client/js/**/*.js';
  * gulp.src接口有其默认的base值, 本例中默认的base值为'client/js', gulp.src的base参数可以修改base值, 本例中base值被修改为'client';
  
所以最后文件被写入 'build/minified_templates/js/bier/schwarzebier.js' 路径中
  
***
  
## gulp.dest(path [, options])

如上例所示,
* gulp.dest接口的path值会替换gulp.src接口的base值

## gulp.task(name [, deps], fn)

## gulp.watch(glob [, opts], tasks) oder gulp.watch(glob [, opts, cb]) ( Notice: cb是callback的简写 )







var gulp = require('gulp');
var changed = require('gulp-changed');
var jscs = require('gulp-jscs');
var uglify = require('gulp-uglify');

var SRC = 'src/*.js';
var DEST = 'dist';

gulp.task('default', function() {
	return gulp.src(SRC)
		.pipe(changed(DEST))
		.pipe(jscs())
		.pipe(uglify())
		.pipe(gulp.dest(DEST));
});
