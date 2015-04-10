/*Libreria de Machine learning*/

!function b(a,c,d){function e(g,h){if(!c[g]){if(!a[g]){var i="function"==typeof require&&require;if(!h&&i)return i(g,!0);if(f)return f(g,!0);throw new Error("Cannot find module '"+g+"'")}var j=c[g]={exports:{}};a[g][0].call(j.exports,function(b){var c=a[g][1][b];return e(c?c:b)},j,j.exports,b,a,c,d)}return c[g].exports}for(var f="function"==typeof require&&require,g=0;g<d.length;g++)e(d[g]);return e}({1:[function(a,b){!function(c){function f(a){var b=this;b.col="undefined"==typeof a.col?-1:a.col,b.value=a.value,b.results=a.results,b.tb=a.tb,b.fb=a.fb}function g(a,b){if("undefined"==typeof a.tb.results&&g(a.tb,b),"undefined"==typeof a.fb.results&&g(a.fb,b),"undefined"!=typeof a.tb.results&&"undefined"!=typeof a.fb.results){var c=[],d=[],e=[];Object.keys(a.tb.results).forEach(function(b){for(var d=0;d<a.tb.results[b];d++)c.push([b]),e.push([b])}),Object.keys(a.fb.results).forEach(function(b){for(var c=0;c<a.fb.results[b];c++)d.push([b]),e.push([b])});var f=1*c.length/e.length,h=k(e)-f*k(c)-(1-f)*k(d);b>h&&(a.tb=void 0,a.fb=void 0,a.results=l(e))}}function h(a,b){if("undefined"!=typeof b.results)return b.results;var e,c=a[b.col];return e=d.isNumber(c)?c>=b.value?b.tb:b.fb:c===b.value?b.tb:b.fb,h(a,e)}function i(a,b){b=b||"","undefined"!=typeof a.results?console.log(a.results):(console.log(a.col+":"+a.value+"? "),c.stdout.write(b+"T->"),i(a.tb,b+"  "),c.stdout.write(b+"F->"),i(a.fb,b+"  "))}function j(a,b){if(0==a.length)return new f;var e,g,i,k,c=b(a),d=0,h=a[0].length-1;for(i=0;h>i;i++){var n={};for(k=0;k<a.length;k++)n[a[k][i]]=1;var o=Object.keys(n);for(k=0;k<o.length;k++){var p=m(a,i,o[k]),q=1*p[0].length/a.length,r=c-q*b(p[0])-(1-q)*b(p[1]);r>d&&p[0].length>0&&p[1].length>0&&(d=r,e=[i,o[k]],g=p)}}if(d>0){var s=j(g[0],b),t=j(g[1],b);return new f({col:e[0],value:e[1],tb:s,fb:t})}return new f({results:l(a)})}function k(a){var f,b=function(a){return Math.log(a)/Math.log(2)},c=l(a),d=0,e=Object.keys(c);for(f=0;f<e.length;f++){var g=1*c[e[f]]/a.length;d-=1*g*b(g)}return d}function l(a){var c,b={};for(c=0;c<a.length;c++){var d=a[c][a[c].length-1];"undefined"==typeof b[d]&&(b[d]=0),b[d]++}return b}function m(a,b,c){var e;e=d.isNumber(c)?function(a){return a[b]>=c}:function(a){return a[b]===c};var h,f=[],g=[];for(h=0;h<a.length;h++)e(a[h])?f.push(a[h]):g.push(a[h]);return[f,g]}var d=a("./utils");d.math,f.prototype.print=function(){var a=this;i(a,"")},DecisionTree=b.exports=function(a){var b=this;b.data=a.data,b.result=a.result},DecisionTree.prototype.build=function(){var d,b=this,c=[];for(d=0;d<b.data.length;d++)c.push(b.data[d]),c[d].push(b.result[d]);return b.tree=j(c,k),b.tree},DecisionTree.prototype.print=function(){var a=this;i(a.tree,"")},DecisionTree.prototype.classify=function(a){var b=this;return h(a,b.tree)},DecisionTree.prototype.prune=function(a){var b=this;g(b.tree,a)},DecisionTree.prototype.getTree=function(){return this.tree}}.call(this,a("0NpzKc"))},{"./utils":12,"0NpzKc":13}],2:[function(a,b){var d=a("./utils").math;HiddenLayer=b.exports=function(a){var b=this;if(b.input=a.input,"undefined"==typeof a.W){var c=1/a.n_in;a.W=d.randMat(a.n_in,a.n_out,-c,c)}"undefined"==typeof a.b&&(a.b=d.zeroVec(a.n_out)),"undefined"==typeof a.activation&&(a.activation=d.sigmoid),b.W=a.W,b.b=a.b,b.activation=a.activation},HiddenLayer.prototype.output=function(a){var b=this;"undefined"!=typeof a&&(b.input=a);var c=d.addMatVec(d.mulMat(b.input,b.W),b.b);return d.activateMat(c,b.activation)},HiddenLayer.prototype.linearOutput=function(a){var b=this;"undefined"!=typeof a&&(b.input=a);var c=d.addMatVec(d.mulMat(b.input,b.W),b.b);return c},HiddenLayer.prototype.backPropagate=function(a){var b=this;if("undefined"==typeof a)throw new Error("No BackPropagation Input.");var c=d.mulMat(a,m.transpose(b.W));return c},HiddenLayer.prototype.sampleHgivenV=function(a){var b=this;"undefined"!=typeof a&&(b.input=a);var c=b.output(),e=d.probToBinaryMat(c);return e}},{"./utils":12}],3:[function(a,b){var d=a("./utils").math;LogisticRegression=b.exports=function(a){var b=this;b.x=a.input,b.y=a.label,b.W=d.zeroMat(a.n_in,a.n_out),b.b=d.zeroVec(a.n_out),b.settings={"log level":1}},LogisticRegression.prototype.train=function(a){var b=this,c=.1,e=200;"undefined"!=typeof a.input&&(b.x=a.input),"undefined"!=typeof a.lr&&(c=a.lr),"undefined"!=typeof a.epochs&&(e=a.epochs);var f,g=1;for(f=0;e>f;f++){var h=d.softmaxMat(d.addMatVec(d.mulMat(b.x,b.W),b.b)),i=d.minusMat(b.y,h),j=d.mulMat(d.transpose(b.x),i),k=d.meanMatAxis(i,0);if(b.W=d.addMat(b.W,d.mulMatScalar(j,c)),b.b=d.addVec(b.b,d.mulVecScalar(k,c)),b.settings["log level"]>0){var l=100*(1*f/e);l>g&&(console.log("LogisticRegression",l.toFixed(0),"% Completed."),g++)}}b.settings["log level"]>0&&console.log("LogisticRegression Final Cross Entropy : ",b.getReconstructionCrossEntropy())},LogisticRegression.prototype.getReconstructionCrossEntropy=function(){var a=this,b=d.softmaxMat(d.addMatVec(d.mulMat(a.x,a.W),a.b)),c=d.mulMatElementWise(a.y,d.activateMat(b,Math.log)),e=d.mulMatElementWise(d.mulMatScalar(d.addMatScalar(a.y,-1),-1),d.activateMat(d.mulMatScalar(d.addMatScalar(b,-1),-1),Math.log)),f=-d.meanVec(d.sumMatAxis(d.addMat(c,e),1));return f},LogisticRegression.prototype.predict=function(a){var b=this;return d.softmaxMat(d.addMatVec(d.mulMat(a,b.W),b.b))},LogisticRegression.prototype.set=function(a,b){var c=this;c.settings[a]=b}},{"./utils":12}],4:[function(a,b){function f(a){return"undefined"==typeof a?d.euclidean:"function"==typeof a?a:"euclidean"===a.type?d.euclidean:"pearson"===a.type?d.pearson:void 0}var d=a("./utils").math;Kmeans=b.exports,Kmeans.cluster=function(a){var b=a.data,c=a.k,d=f(a.distance),g=a.epochs,h=a.init_using_data;h=!0;var j,k,l,m,i=e(b,c,h),n=[];for(k=0;c>k;k++)n.push([]);for(j=0;g>j;j++){for(n=[],k=0;c>k;k++)n.push([]);for(k=0;k<b.length;k++){var o=0;for(l=0;c>l;l++)d(i[l],b[k])<d(i[o],b[k])&&(o=l);n[o].push(k)}for(k=0;c>k;k++){var p=[];for(l=0;l<b[0].length;l++)p.push(0);if(n[k].length>0){for(l=0;l<n[k].length;l++)for(m=0;m<b[0].length;m++)p[m]+=b[n[k][l]][m];for(l=0;l<b[0].length;l++)p[l]/=n[k].length;i[k]=p}}}return{clusters:n,means:i}};var e=function(a,b,c){var e=[];if(c){var f=d.range(a.length);for(f=d.shuffle(f),g=0;b>g;g++)e.push(a[f[g]])}else{var g,h,i=[];for(g=0;g<a[0].length;g++){var j=a[0][g],k=a[0][g];for(h=0;h<a.length;h++)a[h][g]<j&&(j=a[h][g]),a[h][g]>k&&(k=a[h][g]);i.push([j,k])}for(g=0;b>g;g++){var l=[];for(h=0;h<a[0].length;h++)l.push(Math.random()*(i[h][1]-i[h][0])+i[h][0]);e.push(l)}}return e}},{"./utils":12}],5:[function(a,b){function e(a){return"undefined"==typeof a?function(a){var b=10;return Math.exp(-1*a*a/(2*b*b))}:"function"==typeof a?a:"gaussian"===a.type?function(b){var c=a.sigma;return Math.exp(-1*b*b/(2*c*c))}:"none"===a.type?function(){return 1}:void 0}function f(a){return"undefined"==typeof a?d.euclidean:"function"==typeof a?a:"euclidean"===a.type?d.euclidean:"pearson"===a.type?d.pearson:void 0}var d=a("./utils").math;KNN=b.exports=function(a){var b=this;b.data=a.data,b.result=a.result},KNN.prototype.predict=function(a){var j,b=this,c=a.x,d=a.k||3,g=e(a.weightf),h=f(a.distance),i=[];for(j=0;j<b.data.length;j++)i.push([h(c,b.data[j]),j]);i.sort(function(a,b){return a[0]-b[0]});var m,k=0,l=0;for(j=0;d>j;j++){var n=i[j][0],o=i[j][1];m=g(n),k+=m*b.result[o],l+=m}return k/=l}},{"./utils":12}],6:[function(a,b){ml=b.exports,ml.kmeans=a("./kmeans"),ml.KNN=a("./knn"),ml.SVM=a("./svm"),ml.nmf=a("./nmf"),ml.optimize=a("./optimize"),ml.MLP=a("./mlp"),ml.DecisionTree=a("./DecisionTree"),ml.LogisticRegression=a("./LogisticRegression")},{"./DecisionTree":1,"./LogisticRegression":3,"./kmeans":4,"./knn":5,"./mlp":8,"./nmf":9,"./optimize":10,"./svm":11}],7:[function(b,c){m=c.exports,m.randn=function(){var a,b,c;do a=2*Math.random()-1,b=2*Math.random()-1,c=a*a+b*b;while(c>=1||0==c);return c=Math.sqrt(-2*Math.log(c)/c),a*c},m.shape=function(a){var b=a.length,c=a[0].length;return[b,c]},m.addVec=function(a,b){if(a.length===b.length){var d,c=[];for(d=0;d<a.length;d++)c.push(a[d]+b[d]);return c}throw new Error("Length Error : not same.")},m.minusVec=function(a,b){if(a.length===b.length){var d,c=[];for(d=0;d<a.length;d++)c.push(a[d]-b[d]);return c}throw new Error("Length Error : not same.")},m.addMatScalar=function(a,b){var e,f,c=m.shape(a)[0],d=m.shape(a)[1],g=[];for(e=0;c>e;e++){var h=[];for(f=0;d>f;f++)h.push(a[e][f]+b);g.push(h)}return g},m.addMatVec=function(a,b){if(a[0].length===b.length){var d,c=[];for(d=0;d<a.length;d++)c.push(m.addVec(a[d],b));return c}throw new Error("Length Error : not same.")},m.minusMatVec=function(a,b){if(a[0].length===b.length){var d,c=[];for(d=0;d<a.length;d++)c.push(m.minusVec(a[d],b));return c}throw new Error("Length Error : not same.")},m.addMat=function(a,b){if(a.length===b.length&&a[0].length===b[0].length){for(var c=new Array(a.length),d=0;d<a.length;d++){c[d]=new Array(a[d].length);for(var e=0;e<a[d].length;e++)c[d][e]=a[d][e]+b[d][e]}return c}throw new Error("Matrix mismatch.")},m.minusMat=function(a,b){if(a.length===b.length&&a[0].length===b[0].length){for(var c=new Array(a.length),d=0;d<a.length;d++){c[d]=new Array(a[d].length);for(var e=0;e<a[d].length;e++)c[d][e]=a[d][e]-b[d][e]}return c}throw new Error("Matrix mismatch.")},m.transpose=function(a){for(var b=new Array(a[0].length),c=0;c<a[0].length;c++){b[c]=new Array(a.length);for(var d=0;d<a.length;d++)b[c][d]=a[d][c]}return b},m.dotVec=function(a,b){if(a.length===b.length){for(var c=0,d=0;d<a.length;d++)c+=a[d]*b[d];return c}throw new Error("Vector mismatch")},m.outerVec=function(a,b){var c=m.transpose([a]),d=[b];return m.mulMat(c,d)},m.mulVecScalar=function(a,b){var c,d=[];for(c=0;c<a.length;c++)d.push(a[c]*b);return d},m.mulMatScalar=function(a,b){var e,f,c=m.shape(a)[0],d=m.shape(a)[1],g=[];for(e=0;c>e;e++){var h=[];for(f=0;d>f;f++)h.push(a[e][f]*b);g.push(h)}return g},m.mulMatElementWise=function(a,b){if(a.length===b.length&&a[0].length===b[0].length){for(var c=new Array(a.length),d=0;d<a.length;d++)c[d]=new Array(a[0].length);for(var e=0;e<c.length;e++)for(var f=0;f<c[e].length;f++)c[e][f]=a[e][f]*b[e][f];return c}throw new Error("Matrix shape error : not same")},m.mulMat=function(a,b){if(a[0].length===b.length){for(var c=new Array(a.length),d=0;d<a.length;d++)c[d]=new Array(b[0].length);for(var e=m.transpose(b),f=0;f<c.length;f++)for(var g=0;g<c[f].length;g++)c[f][g]=m.dotVec(a[f],e[g]);return c}throw new Error("Array mismatch")},m.sumVec=function(a){for(var b=0,c=a.length;c--;)b+=a[c];return b},m.sumMat=function(a){for(var b=0,c=a.length;c--;)for(var d=0;d<a[0].length;d++)b+=a[c][d];return b},m.sumMatAxis=function(a,b){if(1===b){var d,c=m.shape(a)[0],e=[];for(d=0;c>d;d++)e.push(m.sumVec(a[d]));return e}return mat_T=m.transpose(a),m.sumMatAxis(mat_T,1)},m.meanVec=function(a){return 1*m.sumVec(a)/a.length},m.meanMat=function(a){var b=a.length,c=a[0].length;return 1*m.sumMat(a)/(b*c)},m.meanMatAxis=function(a,b){if(1===b){var d,c=m.shape(a)[0],e=[];for(d=0;c>d;d++)e.push(m.meanVec(a[d]));return e}return mat_T=m.transpose(a),m.meanMatAxis(mat_T,1)},m.squareVec=function(a){var c,b=[];for(c=0;c<a.length;c++)b.push(a[c]*a[c]);return b},m.squareMat=function(a){var c,b=[];for(c=0;c<a.length;c++)b.push(m.squareVec(a[c]));return b},m.minVec=function(a){for(var b=a[0],c=a.length;c--;)a[c]<b&&(b=a[c]);return b},m.maxVec=function(a){for(var b=a[0],c=a.length;c--;)a[c]>b&&(b=a[c]);return b},m.minMat=function(a){for(var b=a[0][0],c=a.length;c--;)for(var d=0;d<a[0].length;d++)a[c][d]<b&&(b=a[c][d]);return b},m.maxMat=function(a){for(var b=a[0][0],c=a.length;c--;)for(var d=0;d<a[0].length;d++)a[c][d]<b&&(b=a[c][d]);return b},m.zeroVec=function(a){for(var b=[];b.length<a;)b.push(0);return b},m.zeroMat=function(a,b){for(var c=[];c.length<a;)c.push(m.zeroVec(b));return c},m.oneVec=function(a){for(var b=[];b.length<a;)b.push(1);return b},m.oneMat=function(a,b){for(var c=[];c.length<a;)c.push(m.oneVec(b));return c},m.randVec=function(a,b,c){b="undefined"!=typeof b?b:0,c="undefined"!=typeof c?c:1;for(var d=[];d.length<a;)d.push(b+(c-b)*Math.random());return d},m.randMat=function(a,b,c,d){c="undefined"!=typeof c?c:0,d="undefined"!=typeof d?d:1;for(var e=[];e.length<a;)e.push(m.randVec(b,c,d));return e},m.randnVec=function(a,b,c){for(var d=[];d.length<a;)d.push(b+c*m.randn());return d},m.randnMat=function(a,b,c,d){for(var e=[];e.length<a;)e.push(m.randnVec(b,c,d));return e},m.identity=function(a){for(var b=new Array(a),c=0;a>c;c++){b[c]=new Array(a);for(var d=0;a>d;d++)b[c][d]=c===d?1:0}return b},m.sigmoid=function(a){var b=1/(1+Math.exp(-a));return 1==b?b=.99999999999999:0==b&&(b=1e-14),b},m.dSigmoid=function(b){return a=m.sigmoid(b),a*(1-a)},m.probToBinaryMat=function(a){var d,e,b=m.shape(a)[0],c=m.shape(a)[1],f=[];for(d=0;b>d;d++){var g=[];for(e=0;c>e;e++)Math.random()<a[d][e]?g.push(1):g.push(0);f.push(g)}return f},m.activateVec=function(a,b){var c,d=[];for(c=0;c<a.length;c++)d.push(b(a[c]));return d},m.activateMat=function(a,b){var e,f,c=m.shape(a)[0],d=m.shape(a)[1],g=[];for(e=0;c>e;e++){var h=[];for(f=0;d>f;f++)h.push(b(a[e][f]));g.push(h)}return g},m.activateTwoVec=function(a,b,c){if(a.length===b.length){for(var d=new Array(a.length),e=0;e<d.length;e++)d[e]=c(a[e],b[e]);return d}throw new Error("Matrix shape error : not same")},m.activateTwoMat=function(a,b,c){if(a.length===b.length&&a[0].length===b[0].length){for(var d=new Array(a.length),e=0;e<a.length;e++)d[e]=new Array(a[0].length);for(var f=0;f<d.length;f++)for(var g=0;g<d[f].length;g++)d[f][g]=c(a[f][g],b[f][g]);return d}throw new Error("Matrix shape error : not same")},m.fillVec=function(a,b){for(var c=[];c.length<a;)c.push(b);return c},m.fillMat=function(a,b,c){for(var d=[];d.length<a;){for(var e=[];e.length<b;)e.push(c);d.push(e)}return d},m.softmaxVec=function(a){var b=m.maxVec(a),c=m.activateVec(a,function(a){return Math.exp(a-b)});return m.activateVec(c,function(a){return a/m.sumVec(c)})},m.softmaxMat=function(a){var c,b=[];for(c=0;c<a.length;c++)b.push(m.softmaxVec(a[c]));return b},m.randInt=function(a,b){var c=Math.random()*(b-a+.9999)+a;return Math.floor(c)},m.normalizeVec=function(a){var b,c=[],d=0;for(b=0;b<a.length;b++)d+=a[b];for(b=0;b<a.length;b++)c.push(1*a[b]/d);return c},m.euclidean=function(a,b){var c,d=0;for(c=0;c<a.length;c++){var e=a[c]-b[c];d+=e*e}return Math.sqrt(d)},m.pearson=function(a,b){for(var c=[],d=[],e=[],f=0;f<a.length;f++)c.push(a[f]*b[f]),d.push(a[f]*a[f]),e.push(b[f]*b[f]);for(var g=0,h=0,i=0,j=0,k=0,f=0;f<a.length;f++)g+=a[f],h+=b[f],i+=c[f],j+=d[f],k+=e[f];var l=a.length*i-g*h,m=a.length*j-g*g,n=a.length*k-h*h,o=Math.sqrt(m*n),p=l/o;return p},m.getNormVec=function(a){var b,c=0;for(b=0;b<a.length;b++)c+=a[b]*a[b];return Math.sqrt(c)},m.gaussian=function(a,b){return b=b||10,Math.exp(-1*a*a/(2*b*b))},m.meanVecs=function(a){var c,b=m.zeroVec(a[0].length);for(c=0;c<a.length;c++)b=m.addVec(b,a[c]);return m.activateVec(b,function(b){return 1*b/a.length})},m.covarianceVecs=function(a){var d,b=m.zeroMat(a[0].length,a[0].length),c=m.meanVecs(a);for(d=0;d<a.length;d++){var e=m.minusVec(a[d],c);b=m.addMat(b,m.mulMat(m.transpose([e]),[e]))}return m.activateMat(b,function(b){return 1*b/(a.length-1)})},m.shuffle=function(a){for(var b=[],c=0;c<a.length;c++)b.push(a[c]);for(var d,e,c=b.length;c;d=parseInt(Math.random()*c),e=b[--c],b[c]=b[d],b[d]=e);return b},m.range=function(a,b,c){var d=[];"undefined"==typeof c&&(c=1),"undefined"==typeof b&&(b=a,a=0);for(var e=a;b>e;e+=c)d.push(e);return d}},{}],8:[function(a,b){var d=a("./utils").math;HiddenLayer=a("./HiddenLayer"),MLP=b.exports=function(a){var b=this;b.x=a.input,b.y=a.label,b.sigmoidLayers=[],b.nLayers=a.hidden_layer_sizes.length,b.settings={"log level":1};var c;for(c=0;c<b.nLayers+1;c++){var e,f;e=0==c?a.n_ins:a.hidden_layer_sizes[c-1],f=0==c?b.x:b.sigmoidLayers[b.sigmoidLayers.length-1].sampleHgivenV();var g;g=c==b.nLayers?new HiddenLayer({input:f,n_in:e,n_out:a.n_outs,activation:d.sigmoid,W:"undefined"==typeof a.w_array?void 0:a.w_array[c],b:"undefined"==typeof a.b_array?void 0:a.b_array[c]}):new HiddenLayer({input:f,n_in:e,n_out:a.hidden_layer_sizes[c],activation:d.sigmoid,W:"undefined"==typeof a.w_array?void 0:a.w_array[c],b:"undefined"==typeof a.b_array?void 0:a.b_array[c]}),b.sigmoidLayers.push(g)}},MLP.prototype.train=function(a){var b=this,c=.6,d=1e3;"undefined"!=typeof a.lr&&(c=a.lr),"undefined"!=typeof a.epochs&&(d=a.epochs);var e,f=1;for(e=0;d>e;e++){var g,h=[];for(h.push(b.x),g=0;g<b.nLayers+1;g++)h.push(b.sigmoidLayers[g].output(h[g]));var i=h[b.nLayers+1],j=new Array(b.nLayers+1);for(j[b.nLayers]=m.mulMatElementWise(m.minusMat(b.y,i),m.activateMat(b.sigmoidLayers[b.nLayers].linearOutput(h[b.nLayers]),m.dSigmoid)),g=b.nLayers-1;g>=0;g--)j[g]=m.mulMatElementWise(b.sigmoidLayers[g+1].backPropagate(j[g+1]),m.activateMat(b.sigmoidLayers[g].linearOutput(h[g]),m.dSigmoid));for(var g=0;g<b.nLayers+1;g++){var k=m.activateMat(m.mulMat(m.transpose(h[g]),j[g]),function(a){return 1*a/b.x.length}),l=m.meanMatAxis(j[g],0);b.sigmoidLayers[g].W=m.addMat(b.sigmoidLayers[g].W,k),b.sigmoidLayers[g].b=m.addVec(b.sigmoidLayers[g].b,l)}if(b.settings["log level"]>0){var n=100*(1*e/d);n>f&&(console.log("MLP",n.toFixed(0),"% Completed."),f+=8)}}b.settings["log level"]>0&&console.log("MLP Final Cross Entropy : ",b.getReconstructionCrossEntropy())},MLP.prototype.getReconstructionCrossEntropy=function(){var a=this,b=a.predict(a.x),c=d.activateTwoMat(a.y,b,function(a,b){return a*Math.log(b)}),e=d.activateTwoMat(a.y,b,function(a,b){return(1-a)*Math.log(1-b)}),f=-d.meanVec(d.sumMatAxis(d.addMat(c,e),1));return f},MLP.prototype.predict=function(a){var b=this,c=a;for(i=0;i<b.nLayers+1;i++)c=b.sigmoidLayers[i].output(c);return c},MLP.prototype.set=function(a,b){var c=this;c.settings[a]=b}},{"./HiddenLayer":2,"./utils":12}],9:[function(a,b){var d=a("./utils"),e=d.math;nmf=b.exports,nmf.factorize=function(a){var j,b=a.features,c=a.matrix,d=a.epochs,f=e.shape(c)[0],g=e.shape(c)[1],h=e.randMat(f,b,0,1),i=e.randMat(b,g,0,1);for(j=0;d>j;j++){e.mulMat(h,i);var l=e.mulMat(e.transpose(h),c),m=e.mulMat(e.mulMat(e.transpose(h),h),i);i=e.activateTwoMat(e.mulMatElementWise(i,l),m,function(a,b){return a/b});var n=e.mulMat(c,e.transpose(i)),o=e.mulMat(e.mulMat(h,i),e.transpose(i));h=e.activateTwoMat(e.mulMatElementWise(h,n),o,function(a,b){return a/b})}return[h,i]}},{"./utils":12}],10:[function(a,b){var d=a("./utils").math;optimize=b.exports,optimize.hillclimb=function(a){var e,b=a.domain,c=a.costf,f=[];for(e=0;e<b.length;e++)f.push(d.randInt(b[e][0],b[e][1]));for(var g,h;;){var e,j,i=[];for(e=0;e<b.length;e++)if(f[e]>b[e][0]){var k=[];for(j=0;j<b.length;j++)k.push(f[j]);k[e]-=1,i.push(k)}else if(f[e]<b[e][1]){var k=[];for(j=0;j<b.length;j++)k.push(f[j]);k[e]+=1,i.push(k)}for(g=c(f),h=g,e=0;e<i.length;e++){var l=c(i[e]);h>l&&(h=l,f=i[e])}if(h===g)break}return f},optimize.anneal=function(a){var i,b=a.domain,c=a.costf,e=a.temperature,f=a.cool,g=a.step,j=[];for(i=0;i<b.length;i++)j.push(d.randInt(b[i][0],b[i][1]));for(;e>.1;){var k=d.randInt(0,b.length-1),l=d.randInt(-g,g),m=[];for(i=0;i<j.length;i++)m.push(j[i]);m[k]+=l,m[k]<b[k][0]&&(m[k]=b[k][0]),m[k]>b[k][1]&&(m[k]=b[k][1]);var n=c(j),o=c(m),p=Math.exp(-1*(o-n)/e);(n>o||Math.random()<p)&&(j=m),e*=f}return j},optimize.genetic=function(a){function s(a){var f,c=d.randInt(0,b.length-1),e=[];for(f=0;f<b.length;f++)e.push(a[f]);return e[c]+=Math.random()<.5?1:-1,e[c]<b[c][0]&&(e[c]=b[c][0]),e[c]>b[c][1]&&(e[c]=b[c][1]),e}function t(a,c){var g,e=d.randInt(0,b.length-2),f=[];for(g=0;e>g;g++)f.push(a[g]);for(g=e;g<b.length;g++)f.push(c[g]);return f}function u(a){var c,b=[0];for(c=0;c<a.length;c++)b.push(b[c]+a[c]);var d=Math.random();for(c=0;c<b.length;c++)if(d>b[c]&&d<=b[c+1])return c;return-1}var i,j,b=a.domain,c=a.costf,e=a.population,f=a.q||.3,g=a.elite||.04*e,h=a.epochs||100,k=[];for(i=0;e>i;i++){var l=[];for(j=0;j<b.length;j++)l.push(d.randInt(b[j][0],b[j][1]));k.push(l)}for(k.sort(function(a,b){return c(a)-c(b)}),i=0;h>i;i++){var m=[];for(j=0;g>j;j++)m.push(k[j]);var n=[];for(j=0;j<k.length;j++)n[j]=f*Math.pow(1-f,j);for(n=d.normalizeVec(n),j=0;j<k.length-g;j++){var o=u(n),p=u(n),q=t(k[o],k[p]),r=s(q);m.push(r)}k=m,k.sort(function(a,b){return c(a)-c(b)})}return k[0]}},{"./utils":12}],11:[function(a,b){function e(a){return"undefined"==typeof a?function(a,b){var c=1;return Math.exp(-1*Math.pow(d.getNormVec(d.minusVec(a,b)),2)/(2*c*c))}:"function"==typeof a?a:"gaussian"===a.type?function(b,c){var e=a.sigma;return Math.exp(-1*Math.pow(d.getNormVec(d.minusVec(b,c)),2)/(2*e*e))}:"linear"===a.type?function(a,b){return d.dotVec(a,b)}:"polynomial"===a.type?function(b,c){var e=a.c,f=a.d;return Math.pow(d.dotVec(b,c)+e,f)}:void 0}var d=a("./utils").math;SVM=b.exports=function(a){var b=this;b.x=a.x,b.y=a.y},SVM.prototype.train=function(a){var b=this,c=a.C||1,f=a.tol||1e-4,g=a.max_passes||20,h=a.alpha_tol||1e-5;b.kernel=e(a.kernel),b.alphas=d.zeroVec(b.x.length),b.b=0;for(var j,i=0;g>i;){var l=0;for(j=0;j<b.x.length;j++){var m=b.f(b.x[j])-b.y[j];if(b.y[j]*m<-f&&b.alphas[j]<c||b.y[j]*m>f&&b.alphas[j]>0){var n=d.randInt(0,b.x.length-1);j==n&&(n=(n+1)%b.x.length);var r,s,o=b.f(b.x[n])-b.y[n],p=b.alphas[j],q=b.alphas[n];if(b.y[j]!==b.y[n]?(r=Math.max(0,b.alphas[n]-b.alphas[j]),s=Math.min(c,c+b.alphas[n]-b.alphas[j])):(r=Math.max(0,b.alphas[n]+b.alphas[j]-c),s=Math.min(c,b.alphas[n]+b.alphas[j])),r===s)continue;var t=2*b.kernel(b.x[j],b.x[n])-b.kernel(b.x[j],b.x[j])-b.kernel(b.x[n],b.x[n]);if(t>=0)continue;if(b.alphas[n]-=1*b.y[n]*(m-o)/t,b.alphas[n]>s?b.alphas[n]=s:b.alphas[n]<r&&(b.alphas[n]=r),Math.abs(b.alphas[n]-q)<h)continue;b.alphas[j]+=b.y[j]*b.y[n]*(q-b.alphas[n]);var u=b.b-m-b.y[j]*(b.alphas[j]-p)*b.kernel(b.x[j],b.x[j])-b.y[n]*(b.alphas[n]-q)*b.kernel(b.x[j],b.x[n]),v=b.b-o-b.y[j]*(b.alphas[j]-p)*b.kernel(b.x[j],b.x[n])-b.y[n]*(b.alphas[n]-q)*b.kernel(b.x[n],b.x[n]);b.b=0<b.alphas[j]&&b.alphas[j]<c?u:0<b.alphas[n]&&b.alphas[n]<c?v:(u+v)/2,l++}}0==l?i++:i=0}},SVM.prototype.predict=function(a){var b=this;return b.f(a)>=0?1:-1},SVM.prototype.f=function(a){var d,b=this,c=0;for(d=0;d<b.x.length;d++)c+=b.alphas[d]*b.y[d]*b.kernel(b.x[d],a);return c+=b.b}},{"./utils":12}],12:[function(a,b){utils=b.exports,utils.math=a("./math"),utils.isNumber=function(a){return!isNaN(parseFloat(a))&&isFinite(a)}},{"./math":7}],13:[function(a,b){function e(){}var d=b.exports={};d.nextTick=function(){var a="undefined"!=typeof window&&window.setImmediate,b="undefined"!=typeof window&&window.postMessage&&window.addEventListener;if(a)return function(a){return window.setImmediate(a)};if(b){var c=[];return window.addEventListener("message",function(a){var b=a.source;if((b===window||null===b)&&"process-tick"===a.data&&(a.stopPropagation(),c.length>0)){var d=c.shift();d()}},!0),function(a){c.push(a),window.postMessage("process-tick","*")}}return function(a){setTimeout(a,0)}}(),d.title="browser",d.browser=!0,d.env={},d.argv=[],d.on=e,d.addListener=e,d.once=e,d.off=e,d.removeListener=e,d.removeAllListeners=e,d.emit=e,d.binding=function(){throw new Error("process.binding is not supported")},d.cwd=function(){return"/"},d.chdir=function(){throw new Error("process.chdir is not supported")}},{}]},{},[6]);


/*Libreria de funciones*/

/*Logistic Regression*/
var classifier;
var instancia;
var test_x;
var resultado;

/*FUNCIONES PARA HACER LA PREDICCIÓN*/
function entrenaClasificador(){
  var x = [
           
[5, 1,  1,  2,  1,  2,  1,  1,  1,  2,  3,  1,  1,  1,  1,  2,  3,  2,  1,  5,  1,  2,  1,  1,  1,  3,  1,  2,  2,  3,  2,  1,  2,  1,  5,  2,  1,  1,  2,  1,  3],
[5, 1,  4,  1,  1,  1,  3,  3,  5,  3,  1,  2,  2,  1,  4,  1,  4,  2,  1,  1,  1,  1,  2,  1,  2,  2,  3,  3,  2,  3,  3,  2,  2,  1,  5,  3,  1,  3,  3,  1,  3],
[5, 2,  1,  1,  1,  2,  2,  1,  3,  2,  2,  3,  3,  2,  1,  2,  3,  2,  1,  2,  1,  1,  2,  2,  2,  3,  3,  3,  2,  3,  3,  3,  4,  1,  5,  3,  1,  3,  3,  1,  5],
[7, 2,  1,  1,  1,  3,  2,  1,  1,  1,  1,  3,  3,  2,  2,  1,  3,  2,  1,  2,  1,  2,  3,  2,  1,  3,  2,  3,  3,  3,  3,  1,  3,  2,  5,  3,  1,  2,  4,  1,  6],
[14,  2,  2,  1,  4,  2,  2,  2,  1,  1,  1,  1,  1,  1,  1,  2,  1,  1,  2,  3,  2,  1,  3,  2,  3,  3,  3,  1,  3,  3,  6,  1,  2,  1,  5,  4,  1,  2,  4,  1,  3],
[1, 2,  1,  1,  3,  1,  1,  5,  1,  1,  1,  1,  1,  1,  1,  2,  3,  1,  1,  1,  2,  2,  1,  3,  1,  2,  1,  3,  3,  3,  3,  1,  2,  1,  6,  1,  3,  2,  3,  1,  6],
[1, 2,  1,  1,  3,  1,  1,  5,  1,  1,  1,  1,  1,  1,  1,  2,  3,  1,  1,  1,  2,  2,  1,  3,  1,  2,  1,  3,  3,  3,  3,  1,  2,  1,  6,  1,  3,  2,  3,  1,  6],
[9, 1,  1,  1,  2,  2,  2,  3,  1,  1,  1,  1,  1,  1,  1,  2,  3,  2,  2,  2,  1,  4,  2,  2,  3,  3,  3,  8,  3,  2,  4,  1,  1,  1,  3,  4,  1,  1,  2,  1,  6],
[9, 2,  1,  1,  2,  1,  1,  1,  1,  1,  3,  1,  2,  1,  1,  2,  3,  1,  1,  1,  1,  5,  1,  1,  3,  3,  2,  2,  1,  3,  2,  2,  1,  1,  2,  2,  1,  2,  4,  1,  2],
[1, 1,  1,  1,  1,  1,  2,  5,  1,  1,  2,  1,  1,  1,  1,  2,  3,  1,  2,  6,  1,  2,  1,  2,  2,  1,  1,  3,  3,  3,  2,  1,  3,  1,  4,  3,  2,  2,  2,  1,  4],
[4, 2,  1,  1,  2,  1,  4,  1,  1,  2,  2,  1,  2,  1,  1,  2,  3,  2,  1,  4,  1,  2,  2,  2,  3,  1,  1,  8,  2,  3,  3,  1,  6,  1,  5,  3,  1,  2,  3,  1,  3],
[5, 1,  1,  1,  3,  1,  2,  2,  1,  1,  1,  1,  1,  1,  1,  2,  3,  1,  2,  5,  1,  3,  1,  3,  2,  2,  3,  1,  2,  3,  3,  1,  3,  1,  4,  1,  1,  1,  3,  1,  4],
[6, 2,  2,  1,  2,  1,  3,  1,  3,  2,  3,  2,  2,  1,  3,  1,  2,  2,  1,  3,  1,  1,  2,  2,  3,  3,  3,  8,  2,  2,  6,  3,  2,  1,  2,  4,  1,  1,  2,  2,  1],
[10,  1,  1,  1,  2,  1,  1,  3,  1,  1,  1,  1,  1,  1,  2,  1,  2,  1,  3,  3,  1,  2,  1,  2,  1,  3,  2,  8,  3,  2,  3,  1,  3,  1,  4,  3,  1,  2,  3,  1,  3],
[7, 1,  1,  1,  1,  3,  1,  1,  1,  3,  3,  1,  2,  2,  1,  1,  4,  2,  1,  2,  1,  1,  3,  1,  1,  3,  2,  3,  3,  3,  3,  1,  2,  1,  4,  3,  1,  4,  4,  1,  6],
[1, 2,  1,  1,  2,  1,  4,  4,  3,  2,  2,  1,  2,  2,  1,  1,  2,  1,  1,  1,  2,  3,  3,  1,  3,  1,  3,  8,  1,  1,  3,  1,  6,  1,  4,  4,  1,  2,  3,  1,  5],
[1, 2,  1,  1,  1,  1,  2,  3,  3,  2,  3,  1,  1,  3,  1,  1,  2,  1,  1,  1,  1,  1,  3,  1,  3,  1,  3,  8,  3,  1,  3,  1,  6,  1,  4,  4,  1,  2,  3,  1,  1],
[9, 2,  2,  1,  2,  3,  4,  1,  3,  1,  3,  2,  2,  2,  2,  2,  2,  2,  1,  3,  1,  1,  1,  2,  3,  3,  3,  8,  2,  1,  6,  3,  2,  1,  2,  4,  1,  1,  3,  2,  3],
[3, 2,  1,  1,  2,  1,  4,  1,  3,  1,  3,  3,  2,  1,  2,  2,  2,  2,  1,  3,  1,  3,  2,  2,  3,  3,  2,  1,  2,  1,  3,  1,  2,  1,  5,  1,  2,  2,  3,  1,  2],
[6, 2,  1,  1,  1,  1,  2,  4,  1,  1,  7,  2,  2,  2,  1,  2,  3,  2,  4,  6,  1,  5,  2,  2,  3,  3,  3,  8,  2,  3,  3,  1,  3,  1,  6,  3,  3,  3,  1,  2,  2],
[6, 2,  1,  1,  2,  1,  1,  3,  1,  2,  2,  1,  2,  1,  1,  2,  3,  1,  1,  2,  1,  3,  1,  2,  3,  3,  2,  3,  3,  3,  3,  1,  4,  1,  6,  3,  3,  2,  4,  1,  6],
[5, 2,  1,  1,  2,  1,  3,  3,  3,  1,  3,  1,  3,  2,  1,  2,  3,  2,  1,  3,  1,  2,  2,  2,  2,  1,  1,  1,  3,  3,  3,  1,  5,  1,  6,  3,  5,  1,  3,  1,  3],
[5, 2,  1,  1,  2,  1,  2,  2,  3,  2,  2,  1,  1,  1,  1,  1,  2,  2,  2,  1,  1,  3,  1,  2,  3,  3,  3,  8,  2,  3,  3,  1,  1,  1,  6,  1,  1,  2,  3,  1,  5],
[1, 2,  1,  1,  1,  1,  1,  2,  1,  1,  3,  2,  3,  1,  1,  2,  3,  2,  2,  4,  1,  1,  1,  1,  2,  3,  2,  3,  3,  3,  3,  1,  2,  1,  4,  3,  2,  2,  3,  1,  2],
[5, 1,  1,  1,  2,  1,  2,  4,  1,  1,  1,  1,  1,  1,  1,  2,  3,  1,  1,  3,  2,  3,  1,  2,  1,  2,  1,  3,  3,  3,  3,  1,  3,  1,  6,  3,  3,  1,  3,  1,  3],
[3, 1,  1,  1,  3,  1,  2,  2,  1,  2,  1,  1,  1,  2,  1,  2,  3,  1,  2,  3,  1,  3,  2,  2,  3,  1,  1,  3,  2,  3,  3,  3,  3,  1,  6,  3,  3,  2,  4,  1,  6],
[2, 1,  1,  1,  1,  1,  1,  1,  3,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  3,  2,  3,  2,  5,  2,  1,  1,  2,  1,  1],
[7, 1,  2,  1,  2,  3,  2,  3,  5,  2,  4,  4,  3,  3,  2,  2,  2,  2,  4,  3,  1,  2,  1,  2,  2,  1,  1,  3,  2,  2,  2,  2,  4,  2,  4,  2,  5,  3,  2,  3,  2],
[3, 1,  2,  2,  2,  2,  2,  2,  3,  2,  3,  2,  2,  1,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  1,  3,  2,  2,  2,  2],
[5, 1,  2,  2,  3,  2,  2,  2,  7,  2,  3,  2,  2,  1,  2,  2,  3,  2,  2,  2,  1,  2,  2,  2,  2,  2,  3,  2,  2,  2,  3,  2,  2,  3,  2,  1,  2,  3,  2,  2,  2],
[7, 2,  1,  2,  2,  2,  3,  2,  1,  3,  5,  3,  2,  1,  3,  2,  2,  2,  3,  2,  2,  3,  2,  2,  3,  2,  2,  2,  3,  2,  2,  2,  3,  2,  2,  1,  2,  3,  2,  2,  2],
[6, 2,  3,  1,  3,  3,  4,  5,  8,  2,  7,  7,  6,  6,  4,  2,  4,  1,  5,  6,  2,  4,  3,  3,  3,  2,  3,  6,  3,  3,  5,  2,  4,  5,  4,  3,  5,  3,  2,  1,  6],
[2, 2,  4,  1,  3,  2,  2,  3,  5,  2,  3,  3,  2,  2,  2,  2,  2,  1,  2,  2,  2,  3,  2,  2,  2,  3,  2,  3,  2,  2,  3,  2,  2,  2,  6,  1,  3,  2,  2,  2,  2],
[5, 1,  1,  2,  3,  3,  2,  2,  3,  2,  3,  3,  2,  2,  3,  2,  2,  2,  2,  2,  2,  4,  2,  3,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2],
[3, 2,  1,  2,  2,  3,  1,  3,  5,  3,  2,  2,  2,  2,  4,  2,  2,  2,  2,  3,  2,  2,  2,  3,  2,  3,  3,  3,  3,  2,  2,  2,  2,  2,  2,  1,  2,  5,  2,  2,  2],
[8, 2,  3,  2,  2,  2,  3,  2,  3,  3,  2,  2,  2,  1,  2,  2,  2,  1,  2,  2,  2,  2,  2,  2,  2,  2,  2,  3,  2,  3,  2,  2,  2,  3,  2,  3,  2,  2,  4,  2,  2],
[4, 2,  3,  2,  2,  3,  2,  2,  5,  2,  2,  2,  2,  1,  2,  2,  2,  1,  3,  3,  1,  2,  3,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  3,  1,  2,  2,  2,  2,  2],
[5, 1,  1,  1,  2,  1,  3,  1,  3,  2,  3,  4,  3,  2,  1,  2,  4,  2,  1,  2,  1,  2,  1,  1,  2,  3,  1,  1,  2,  3,  3,  1,  3,  1,  6,  1,  3,  1,  2,  1,  2],
[6, 1,  1,  1,  2,  2,  2,  2,  5,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  1,  2,  2,  2,  2,  2,  2,  2,  4,  2,  2,  2,  2,  1,  2,  2,  3,  2,  2],
[5, 1,  2,  1,  3,  3,  4,  5,  8,  2,  7,  7,  7,  6,  4,  2,  2,  2,  5,  6,  1,  5,  3,  4,  1,  2,  3,  8,  2,  3,  6,  3,  5,  6,  6,  4,  4,  5,  3,  4,  6],
[4, 2,  3,  2,  4,  3,  3,  5,  8,  3,  7,  6,  7,  6,  4,  2,  4,  2,  5,  5,  2,  5,  3,  4,  3,  3,  2,  8,  3,  3,  7,  3,  6,  6,  4,  4,  6,  5,  4,  4,  6],
[7, 1,  4,  2,  2,  3,  4,  4,  8,  3,  7,  4,  7,  6,  3,  2,  2,  2,  4,  5,  2,  2,  3,  3,  3,  3,  2,  8,  3,  3,  6,  3,  6,  6,  6,  4,  6,  4,  4,  4,  6],
[7, 1,  4,  2,  2,  3,  4,  4,  8,  3,  7,  4,  7,  6,  3,  2,  2,  2,  4,  5,  2,  2,  3,  3,  3,  3,  2,  8,  3,  3,  6,  3,  6,  6,  6,  4,  6,  4,  4,  4,  6],
[7, 1,  4,  2,  2,  3,  4,  4,  8,  3,  7,  4,  7,  6,  3,  2,  2,  2,  4,  5,  2,  2,  3,  3,  3,  3,  2,  8,  3,  3,  6,  3,  6,  6,  6,  4,  6,  4,  4,  4,  6],
[7, 1,  4,  2,  2,  3,  4,  4,  8,  3,  7,  4,  7,  6,  3,  2,  2,  2,  4,  5,  2,  2,  3,  3,  3,  3,  2,  8,  3,  3,  6,  3,  6,  6,  6,  4,  6,  4,  4,  4,  6],
[7, 1,  4,  2,  2,  3,  4,  4,  8,  3,  7,  4,  7,  6,  3,  2,  2,  2,  4,  5,  2,  2,  3,  3,  3,  3,  2,  8,  3,  3,  6,  3,  6,  6,  6,  4,  3,  4,  2,  4,  2],
[6, 1,  3,  2,  2,  3,  4,  3,  3,  3,  3,  4,  2,  2,  4,  2,  1,  2,  4,  3,  2,  2,  2,  3,  2,  2,  2,  2,  2,  1,  2,  1,  3,  6,  3,  1,  6,  1,  2,  2,  2],
[5, 1,  4,  2,  3,  3,  2,  2,  3,  2,  2,  3,  5,  1,  3,  2,  3,  2,  2,  3,  1,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  3,  4,  2,  2,  1,  5,  2,  2,  2,  2],
[6, 2,  2,  2,  3,  1,  3,  3,  3,  2,  2,  2,  2,  1,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  1,  2,  2,  2,  2,  2],
[12,  2,  2,  2,  2,  2,  2,  2,  5,  1,  3,  4,  2,  1,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  1,  2,  2,  2,  2,  2],
[12,  2,  2,  2,  2,  2,  2,  2,  5,  1,  3,  4,  2,  1,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  1,  2,  2,  2,  2,  2],
[12,  2,  2,  2,  2,  2,  2,  2,  5,  1,  3,  4,  2,  1,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  1,  1,  2,  4,  4,  1,  2],
[10,  2,  3,  2,  2,  2,  2,  4,  7,  2,  2,  4,  3,  1,  2,  2,  4,  2,  2,  3,  1,  2,  1,  3,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  1,  2,  3,  2,  2,  2],
[10,  2,  3,  2,  2,  2,  2,  4,  7,  2,  2,  4,  3,  1,  2,  2,  4,  2,  2,  3,  1,  2,  1,  3,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,  1,  4,  3,  1,  1,  2],
[2, 1,  3,  1,  1,  2,  2,  1,  7,  1,  5,  3,  2,  2,  2,  2,  3,  1,  2,  3,  2,  2,  1,  2,  2,  2,  2,  3,  1,  2,  2,  2,  2,  2,  2,  1,  3,  2,  2,  2,  2],
[2, 1,  3,  1,  1,  2,  2,  1,  7,  1,  5,  3,  2,  2,  2,  2,  3,  1,  2,  3,  2,  2,  1,  2,  2,  2,  2,  8,  3,  2,  5,  3,  2,  6,  2,  4,  1,  2,  3,  1,  2],
[6, 2,  2,  2,  2,  2,  2,  3,  3,  2,  2,  3,  3,  1,  1,  2,  3,  2,  2,  2,  1,  2,  3,  2,  2,  1,  1,  2,  2,  2,  2,  3,  2,  2,  2,  1,  2,  4,  2,  2,  2],
[5, 1,  3,  2,  3,  3,  2,  2,  5,  2,  2,  6,  2,  1,  2,  2,  3,  2,  2,  2,  2,  2,  3,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  4,  2,  1,  2,  2,  3,  2,  2],
[6, 1,  2,  1,  2,  2,  2,  4,  3,  2,  2,  2,  3,  1,  2,  2,  4,  2,  2,  2,  2,  1,  2,  2,  2,  3,  2,  2,  2,  2,  2,  3,  2,  2,  2,  4,  2,  2,  2,  1,  3],
[7, 2,  2,  1,  2,  2,  2,  1,  1,  3,  3,  3,  3,  2,  1,  1,  2,  2,  1,  2,  1,  1,  2,  1,  3,  1,  1,  8,  2,  1,  6,  2,  2,  1,  3,  4,  1,  1,  2,  1,  1],
[9, 2,  3,  2,  3,  3,  3,  5,  8,  3,  2,  2,  2,  1,  2,  2,  3,  2,  2,  2,  2,  2,  2,  3,  2,  2,  3,  2,  3,  2,  2,  2,  2,  2,  2,  3,  2,  4,  2,  1,  2],
[4, 2,  3,  2,  2,  2,  2,  3,  3,  2,  2,  2,  2,  1,  3,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  1,  2,  5,  2,  1,  4],
[6, 1,  1,  1,  2,  1,  4,  1,  1,  2,  4,  3,  3,  3,  1,  2,  3,  1,  1,  2,  2,  2,  1,  1,  1,  3,  1,  3,  2,  3,  3,  2,  4,  1,  6,  1,  1,  1,  2,  1,  1],
[5, 1,  2,  2,  3,  2,  2,  3,  3,  2,  3,  3,  3,  5,  2,  2,  2,  2,  3,  2,  1,  2,  3,  2,  2,  3,  2,  2,  2,  2,  2,  3,  4,  2,  3,  1,  2,  2,  2,  1,  5],
[6, 2,  1,  1,  2,  1,  2,  1,  3,  3,  5,  1,  3,  4,  1,  2,  4,  1,  1,  3,  1,  2,  1,  1,  1,  3,  1,  1,  2,  3,  3,  2,  4,  1,  6,  1,  2,  1,  2,  1,  1],
[5, 1,  2,  1,  2,  1,  3,  1,  5,  2,  4,  5,  3,  6,  1,  2,  3,  2,  1,  2,  1,  2,  2,  2,  1,  1,  1,  3,  2,  3,  3,  1,  2,  1,  5,  3,  2,  1,  2,  3,  6],
[5, 1,  2,  2,  3,  2,  2,  3,  3,  2,  3,  3,  3,  5,  2,  2,  2,  2,  3,  4,  1,  2,  3,  2,  2,  2,  1,  6,  2,  2,  6,  3,  4,  4,  3,  2,  5,  4,  3,  1,  3],
[5, 2,  2,  2,  2,  3,  1,  2,  3,  3,  2,  2,  2,  1,  2,  2,  1,  2,  2,  3,  2,  1,  2,  2,  3,  2,  2,  2,  2,  2,  2,  2,  2,  3,  3,  4,  2,  2,  4,  1,  3],
[7, 2,  3,  2,  2,  2,  3,  2,  5,  3,  2,  4,  2,  3,  2,  2,  2,  1,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  1,  2,  2,  2,  1,  2],
[5, 2,  2,  2,  2,  3,  2,  2,  3,  3,  2,  4,  2,  1,  2,  2,  2,  2,  2,  4,  2,  3,  2,  2,  2,  2,  2,  2,  2,  3,  2,  2,  2,  2,  2,  1,  2,  2,  3,  1,  1],
[5, 1,  2,  2,  4,  1,  2,  2,  5,  2,  2,  2,  2,  1,  2,  2,  2,  2,  2,  4,  1,  2,  3,  2,  2,  2,  2,  2,  2,  3,  3,  2,  2,  2,  2,  1,  3,  3,  3,  1,  1],
[5, 2,  1,  2,  2,  3,  3,  1,  1,  2,  2,  4,  4,  1,  1,  2,  4,  1,  2,  2,  1,  1,  3,  1,  1,  2,  2,  1,  2,  3,  3,  3,  1,  1,  4,  1,  1,  1,  3,  2,  1],
[6, 2,  3,  2,  2,  2,  2,  2,  5,  2,  3,  2,  2,  1,  3,  2,  2,  2,  3,  2,  1,  2,  3,  2,  2,  2,  3,  3,  2,  2,  2,  2,  2,  2,  2,  1,  3,  3,  2,  1,  2],
[7, 2,  2,  1,  2,  2,  2,  2,  7,  2,  5,  2,  3,  1,  1,  2,  2,  2,  2,  2,  1,  2,  2,  2,  2,  2,  2,  3,  3,  2,  2,  3,  2,  2,  2,  3,  2,  1,  2,  1,  4],
[7, 2,  1,  1,  2,  1,  2,  1,  5,  2,  5,  1,  3,  2,  1,  2,  3,  1,  1,  2,  1,  1,  1,  1,  2,  2,  1,  2,  2,  3,  2,  2,  2,  1,  4,  2,  2,  1,  2,  1,  1],
[4, 2,  4,  1,  4,  3,  3,  5,  8,  3,  7,  6,  7,  6,  4,  2,  4,  2,  5,  6,  1,  5,  3,  4,  3,  3,  3,  2,  2,  2,  3,  2,  2,  2,  2,  1,  2,  3,  2,  1,  2],
[5, 1,  2,  1,  2,  1,  2,  2,  3,  3,  2,  3,  2,  1,  3,  2,  2,  2,  2,  5,  1,  2,  2,  2,  2,  1,  1,  3,  3,  2,  2,  2,  2,  2,  2,  1,  2,  3,  2,  1,  2],
[7, 1,  1,  1,  1,  2,  3,  1,  1,  3,  4,  2,  3,  1,  1,  2,  4,  2,  1,  2,  1,  1,  1,  1,  1,  1,  1,  1,  3,  3,  3,  2,  2,  1,  4,  1,  1,  1,  1,  2,  1],
[5, 2,  1,  1,  2,  2,  2,  1,  5,  3,  5,  2,  4,  2,  1,  2,  4,  2,  1,  3,  1,  2,  1,  1,  1,  1,  1,  1,  2,  3,  3,  3,  1,  1,  4,  1,  1,  1,  3,  1,  2],
[9, 2,  1,  1,  1,  1,  2,  2,  5,  3,  4,  3,  3,  4,  1,  2,  4,  2,  3,  1,  1,  1,  3,  2,  2,  1,  1,  2,  2,  3,  2,  2,  2,  1,  4,  2,  1,  1,  1,  4,  1],
[7, 1,  1,  1,  2,  1,  2,  4,  1,  1,  2,  1,  1,  1,  1,  2,  1,  2,  4,  4,  1,  1,  1,  2,  2,  2,  3,  3,  2,  3,  3,  3,  3,  1,  5,  3,  1,  1,  3,  1,  3],
[7, 2,  1,  1,  2,  1,  1,  1,  3,  1,  1,  1,  1,  1,  1,  1,  3,  2,  1,  2,  1,  3,  1,  2,  1,  3,  2,  2,  2,  3,  3,  1,  6,  1,  4,  2,  1,  1,  3,  1,  2],
[5, 2,  1,  1,  1,  2,  4,  1,  3,  2,  5,  4,  4,  5,  4,  1,  4,  2,  1,  1,  1,  1,  2,  1,  2,  1,  3,  1,  2,  3,  1,  2,  1,  1,  3,  3,  1,  1,  2,  2,  1],
[4, 2,  1,  1,  3,  3,  2,  2,  1,  1,  1,  1,  1,  1,  1,  2,  3,  2,  2,  2,  1,  4,  2,  2,  2,  3,  3,  1,  2,  3,  3,  1,  3,  2,  6,  1,  1,  2,  3,  1,  6],
[8, 1,  1,  1,  2,  1,  3,  1,  3,  3,  4,  4,  4,  3,  3,  2,  4,  2,  1,  2,  1,  1,  2,  1,  1,  1,  3,  3,  2,  3,  3,  2,  3,  1,  4,  1,  2,  1,  2,  1,  1],
[6, 2,  4,  1,  1,  2,  2,  1,  7,  2,  4,  4,  4,  4,  1,  2,  2,  2,  1,  1,  1,  1,  3,  1,  3,  1,  3,  8,  1,  1,  6,  2,  2,  1,  3,  4,  1,  1,  1,  1,  1],
[8, 1,  1,  1,  1,  2,  2,  4,  7,  1,  2,  3,  1,  1,  3,  2,  3,  2,  3,  5,  2,  3,  3,  3,  2,  2,  1,  5,  3,  2,  4,  3,  3,  3,  5,  1,  3,  4,  3,  2,  4],
[5, 1,  2,  2,  2,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  2,  3,  1,  1,  2,  1,  2,  1,  3,  1,  3,  3,  6,  3,  2,  6,  2,  2,  1,  2,  1,  2,  2,  3,  1,  1],
          ];
  var y = [
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1],
           [0, 1]
          ];
           
  classifier = new ml.LogisticRegression({'input' : x,
                                              'label' : y,
                                              'n_in' : 7,
                                              'n_out' : 2
                                             });
      
  classifier.train({'lr' : 0.6,
                    'epochs' : 2000
                   });
  
}//end of entrenaClasificador

//Ejemplo de instancias a clasificar. En el ejemplo hay tres instancias.
//Por tal razón la antrada es un arreglo de arreglos. Esto debe hacerse
//incluso si sólo es una instancia, es decir, un arreglo que contiene un
//arreglo.
function clasificaInstancia(){
  test_x = [[1, 1, 0, 0, 0, 0],
            [0, 0, 0, 1, 1, 0],
            [1, 1, 1, 1, 1, 0]];
          
  document.write("Result : ", classifier.predict(test_x));
}//end of clasificaInstancia

/*FUNCIONES PARA CREAR LA INSTANCIA*/

function creaYClasificaInstancia(){
  var coleccionPreguntas = document.getElementById("preguntas").getElementsByTagName("div");
  instancia = [];
  for(var i=0; i<coleccionPreguntas.length; i++){
    instancia.push(obtieneRespuesta(coleccionPreguntas[i].id));
  }//end for colección
  
  //La instancia se convierte en un arreglo de arreglos para poder ingresarlo al clasificador.
  //Esto se realiza para cumplir con los requerimientos de entrada según la documentación.
  instancia = [instancia];        
  var clasificacion = classifier.predict(instancia);
 
  if(clasificacion[0] > clasificacion[1]){
    resultado = "¡Cuidado!, usted está en RIESGO de desertar de la universidad.";
  }
  else{
    resultado = "Usted NO está en riesgo de desertar de la universidad.";
  }
  alert(resultado);
  
}//end of creaInstancia

function obtieneRespuesta(radioGroupId){
  var pregunta = document.getElementById(radioGroupId);
  var opciones = pregunta.getElementsByTagName("input");
  var val;
  for(var i=0; i<opciones.length; i++){
    if(opciones[i].checked){
      val = opciones[i].value;
      break;
    }//end if
  }//end for
  
  return val;
}//end of 

/*Pagina html*/

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>Pagina para uso de PIWEKA</title>
</head>

  

<body background="verde.jpg">
<h1>Descripción</h1>
   <font face="Comic Sans MS">Encuesta que influyen en la No Deserción Universitaria.</font>
  
  <tr> 
    <br></br><td>1.-Seleccione su edad</td>
    <tr><td><form action>
    <select name="edad">
    <option value="17"> 17</option>
    <option value="18"> 18</option>
    <option value="19"> 19</option>
    <option value="20"> 20</option>
    <option value="21"> 21</option>
    <option value="22"> 22</option>
    <option value="23"> 23</option>
    <option value="24"> 24</option>
    <option value="25"> 25</option>
    <option value="26"> 26</option>
    <option value="27"> 27</option>
    <option value="28"> 28</option>
    <option value="29"> 29</option>
    <option value="30"> 30</option>
    </select>
    <br></br>
    </form></td></tr>
  </tr>
  <tr> <br></br>
    <td>2.-Selecciona tu género</td><br></br>
    <tr><td><input type="radio" name="sexo" value="masculino"> Masculino </td></tr>
    <tr><td><input type="radio" name="sexo" value="femenino"> Femenino</td></tr>
  </tr>
  <br></br>
  <tr><br></br>
    <td>3.-¿Cuál es tu estado civil?</td><br></br>
    <td><input type="radio" name="estado" value="soltero"> Soltero</td><br></br>
    <td><input type="radio" name="estado" value="casado"> Casado</td><br></br>
    <td><input type="radio" name="estado" value="viudo"> Viudo</td><br></br>
    <td><input type="radio" name="estado" value="divorciado"> Divorciado</td><br></br>
  </tr><br></br>
  <tr>
    <td>4.-Tipo de escuela</td><br></br>
    <td><input type="radio" name="escuela" value="publica"> Pública</td><br></br>
    <td><input type="radio" name="escuela" value="privada"> Privada</td><br></br>
  </tr>
  <tr><br></br>
    <td>5.-Promedio con el cuál ingresaste a la Universidad(Seleccione el aproximado)</td><br></br>
    <td><form action>
    <select name="promedio">
    <option value="7"> 7</option>
    <option value="8"> 8</option>
    <option value="9"> 9</option>
    <option value="10">10</option>
    </select>
    <br></br>
    </form></td>
  </tr>
   <tr><br></br> 
    <td>6.-¿Porque ingresaste a la carrera?</td><br></br>
    <td><input type="radio" name="carrera" value="gusto"> Me gusta </td><br></br>
    <td><input type="radio" name="carrera" value="padres"> Mis padres me obligaron</td><br></br>
    <td><input type="radio" name="carrera" value="obligacion"> Obligación</td><br></br>
  </tr>
  <tr><br></br>
    <td>7.-Factores que infieren en el desempeño académico.</td><br></br>
    <td><input type="radio" name="factores" value="ninguno"> Ninguno</td><br></br>
    <td><input type="radio" name="factores" value="dinero"> Dinero</td><br></br>
    <td><input type="radio" name="factores" value="desinteres"> Desinterés</td><br></br>
    <td><input type="radio" name="factores" value="trabajo"> Trabajo</td><br></br>
  </tr>
  <tr> <br></br>
    <td>8.-Tiempo dedicado a estudiar.</td><br></br>
    <td><input type="radio" name="horas" value="1"> 1hr. </td><br></br>
    <td><input type="radio" name="horas" value="2"> 2hrs. </td><br></br>
    <td><input type="radio" name="horas" value="3"> 3hrs. </td><br></br>
    <td><input type="radio" name="horas" value="4"> 4hrs. </td><br></br>
    <td><input type="radio" name="horas" value="masde"> Más de 5hrs. </td><br></br>
  </tr>
  <tr><br></br>
    <td>9.-Frecuencias de inasistencias al mes.</td><br></br>
    <td><input type="radio" name="faltas" value="1"> 1 al mes.</td><br></br>
    <td><input type="radio" name="faltas" value="2"> 2 al mes.</td><br></br>
    <td><input type="radio" name="faltas" value="3"> 3 al mes.</td><br></br>
    <td><input type="radio" name="faltas" value="5"> 5 al mes.</td><br></br>
    <td><input type="radio" name="faltas" value="7"> 7 a mes. </td><br></br>
    <td><input type="radio" name="faltas" value="mas"> Más de 8 al mes. </td> <br></br>
  </tr>
  <tr><br></br>
    <td>10.-La universidad que elegiste ¿Porque fué?</td><br></br>
    <td><input type="radio" name="eleccion" value="primera"> Primera opción.</td><br></br>
    <td><input type="radio" name="eleccion" value="segunda"> Segunda opción.</td><br></br>
    <td><input type="radio" name="eleccion" value="ultima"> Última opción.</td><br></br>
  </tr>
  <tr> <br></br>
    <td>11.-Frecuencia de materias reprobadas.</td><br></br>
    <td><input type="radio" name="reprobadas" value="1"> 1 </td><br></br>
    <td><input type="radio" name="reprobadas" value="2"> 2 </td><br></br>
    <td><input type="radio" name="reprobadas" value="3"> 3 </td><br></br>
    <td><input type="radio" name="reprobadas" value="4"> 4 </td><br></br>
    <td><input type="radio" name="reprobadas" value="5"> 5 </td><br></br>
    <td><input type="radio" name="reprobadas" value="6"> 6 </td><br></br>
    <td><input type="radio" name="reprobadas" value="ninguna"> Ninguna </td> <br></br>
  </tr>
  <tr> <br></br>
    <td>12.-Frecuencia de materias dadas de baja.</td><br></br>
    <td><input type="radio" name="baja" value="1"> 1 </td><br></br>
    <td><input type="radio" name="baja" value="2"> 2 </td><br></br>
    <td><input type="radio" name="baja" value="3"> 3 </td><br></br>
    <td><input type="radio" name="baja" value="4"> 4 </td><br></br>
    <td><input type="radio" name="baja" value="5"> 5 </td><br></br>
    <td><input type="radio" name="baja" value="6"> 6 </td><br></br>
    <td><input type="radio" name="baja" value="ninguna"> Ninguna </td> <br></br>
  </tr>
  <tr> <br></br>
    <td>13.-Frecuencia con la que recursas materias.</td><br></br>
    <td><input type="radio" name="recursa" value="1"> 1 </td><br></br>
    <td><input type="radio" name="recursa" value="2"> 2 </td><br></br>
    <td><input type="radio" name="recursa" value="3"> 3 </td><br></br>
    <td><input type="radio" name="recursa" value="4"> 4 </td><br></br>
    <td><input type="radio" name="recursa" value="5"> 5 </td><br></br>
    <td><input type="radio" name="recursa" value="6"> 6 </td><br></br>
    <td><input type="radio" name="recursa" value="ninguna"> Ninguna </td> <br></br>
  </tr>
  <tr> <br></br>
    <td>14.-Frecuencia de extraordinarios realizados.</td><br></br>
    <td><input type="radio" name="extra" value="1"> 1 </td><br></br>
    <td><input type="radio" name="extra" value="2"> 2 </td><br></br>
    <td><input type="radio" name="extra" value="3"> 3 </td><br></br>
    <td><input type="radio" name="extra" value="4"> 4 </td><br></br>
    <td><input type="radio" name="extra" value="5"> 5 </td><br></br>
    <td><input type="radio" name="extra" value="6"> 6 </td><br></br>
    <td><input type="radio" name="extra" value="ninguna"> Ninguna </td> <br></br>
  </tr>
  <tr> <br></br>
    <td>15.-Tipo de transporte para ir a la Universidad.</td><br></br>
    <td><input type="radio" name="transporte" value="publico"> Transporte público </td><br></br>
    <td><input type="radio" name="transporte" value="privado"> Auto propio </td><br></br>
    <td><input type="radio" name="transporte" value="caminando"> Caminando </td><br></br>
    <td><input type="radio" name="transporte" value="bicicleta"> Biclicleta/Motocicleta </td><br></br>
  </tr>
   <tr> <br></br>
    <td>16.- Tiempo de traslado de casa7trabajo a la Universidad</td><br></br>
    <td><input type="radio" name="tiempo" value="30"> 30 min. </td><br></br>
    <td><input type="radio" name="tiempo" value="40"> 40 min.. </td><br></br>
    <td><input type="radio" name="tiempo" value="50"> 50 min. </td><br></br>
    <td><input type="radio" name="tiempo" value="1"> 1 hr. </td><br></br>
    <td><input type="radio" name="tiempo" value="1media"> 1 hr 30 min. </td><br></br>
    <td><input type="radio" name="tiempo" value="2"> 2 hrs. </td><br></br>
    <td><input type="radio" name="tiempo" value="masde"> Más de 2hrs. </td><br></br>
  </tr>
  <tr><br></br>
    <td>17.- Motivos por los cuales llegas tarde a la Universidad.</td><br></br>
    <td><input type="radio" name="motivos" value="no"> No llego tarde.</td><br></br>
    <td><input type="radio" name="motivos" value="trabajo"> Trabajo</td><br></br>
    <td><input type="radio" name="motivos" value="trafico"> Trafico(A veces)</td><br></br>
    <td><input type="radio" name="motivos" value="trabajo"> Falta de interés</td><br></br>
  </tr>
  <tr><br></br>
    <td>18.- Turno en que asistes a la universidad.</td><br></br>
    <td><input type="radio" name="turno" value="matutino"> Matutino</td><br></br>
    <td><input type="radio" name="turno" value="vespertino"> Vespertino</td><br></br>
  </tr>
  <tr> <br></br>
    <td>19.-Tiempo dedicado a estudiar.</td><br></br>
    <td><input type="radio" name="horas" value="1"> 1hr. </td><br></br>
    <td><input type="radio" name="horas" value="2"> 2hrs. </td><br></br>
    <td><input type="radio" name="horas" value="3"> 3hrs. </td><br></br>
    <td><input type="radio" name="horas" value="4"> 4hrs. </td><br></br>
    <td><input type="radio" name="horas" value="masde"> Más de 5hrs. </td><br></br>
  </tr>
   <tr> <br></br>
    <td>20.-Frecuencia con que asistes a la biblioteca.</td><br></br>
    <td><input type="radio" name="biblio" value="1"> 1 vez.</td><br></br>
    <td><input type="radio" name="biblio" value="2"> 2 veces.</td><br></br>
    <td><input type="radio" name="biblio" value="3"> 3 veces.</td><br></br>
    <td><input type="radio" name="biblio" value="4"> 4 veces.</td><br></br>
    <td><input type="radio" name="biblio" value="5"> 5 veces.</td><br></br>
    <td><input type="radio" name="biblio" value="ninguna"> Ninguna </td> <br></br>
  </tr>
  <tr><br></br>
    <td>21.- ¿La universidad cuenta con internet?</td><br></br>
    <td><input type="radio" name="internet" value="si"> Si</td><br></br>
    <td><input type="radio" name="internet" value="no"> No</td><br></br>
  </tr>
  <tr> <br></br>
    <td>22.-Frecuencia con la que ocupas la computadora de forma productiva(Proyectos, tareas, investigaciones).</td><br></br>
    <td><input type="radio" name="frec" value="1"> 1 hr.</td><br></br>
    <td><input type="radio" name="frec" value="2"> 2 hrs.</td><br></br>
    <td><input type="radio" name="frec" value="3"> 3 hrs.</td><br></br>
    <td><input type="radio" name="frec" value="4"> 4 hrs.</td><br></br>
    <td><input type="radio" name="frec" value="5"> 5 hrs.</td><br></br>
    <td><input type="radio" name="frec" value="mas">  Mas de 5 hrs.</td> <br></br>
  </tr>
  <tr><br></br>
    <td>23.- Problemas con profesor.</td><br></br>
    <td><input type="radio" name="problemas" value="calificaciones"> Motivos de calificaciones </td><br></br>
    <td><input type="radio" name="problemas" value="irrumpir"> Irrumpe en la clase </td><br></br>
    <td><input type="radio" name="problemas" value="ninguno"> Ninguno </td><br></br>
  </tr>
  <tr><br></br>
    <td>24.- Promedio de la universidad.</td><br></br>
    <td><input type="radio" name="prom" value="7"> 7</td><br></br>
    <td><input type="radio" name="prom" value="8"> 8</td><br></br>
    <td><input type="radio" name="prom" value="9"> 9</td><br></br>
    <td><input type="radio" name="prom" value="10"> 10</td><br></br>
  </tr>
   <tr><br></br>
    <td>25.- Condición laboral actual.</td><br></br>
    <td><input type="radio" name="trabaja" value="no"> Ninguno</td><br></br>
    <td><input type="radio" name="trabaja" value="busca"> En busca de empleo</td><br></br>
    <td><input type="radio" name="trabaja" value="trabajo"> Trabajo</td><br></br>
  </tr>
  <tr><br></br>
    <td>26.- Equipo de cómputo.</td><br></br>
    <td><input type="radio" name="equipo" value="ninguno"> Ninguno</td><br></br>
    <td><input type="radio" name="equipo" value="escritorio"> Escritorio</td><br></br>
    <td><input type="radio" name="equipo" value="laptop"> Laptop</td><br></br>
  </tr>
  <tr><br></br>
    <td>27.- Tipo de internet.</td><br></br>
    <td><input type="radio" name="internet" value="no"> No tengo</td><br></br>
    <td><input type="radio" name="internet" value="propio"> Propio</td><br></br>
    <td><input type="radio" name="internet" value="compartido"> Compartido</td><br></br>
  </tr>
  <tr><br></br>
    <td>28.- Obtención de ingersos para gastos escolares.</td><br></br>
    <td><input type="radio" name="gastos" value="padre"> Padre</td><br></br>
    <td><input type="radio" name="gastos" value="madre"> Madre</td><br></br>
    <td><input type="radio" name="gastos" value="ambos"> Ambos</td><br></br>
    <td><input type="radio" name="gastos" value="abuelos"> Abuelos</td><br></br>
    <td><input type="radio" name="gastos" value="tios"> Tíos</td><br></br>
    <td><input type="radio" name="gastos" value="esposa"> Esposa(o)</td><br></br>
    <td><input type="radio" name="gastos" value="beca"> Beca</td><br></br>
    <td><input type="radio" name="gastos" value="propio"> Propio</td><br></br>
  </tr>
  <tr><br></br>
    <td>29.- Pagos de colegiatura en tiempo y forma.</td><br></br>
    <td><input type="radio" name="colegiatura" value="nunca"> Nunca</td><br></br>
    <td><input type="radio" name="colegiatura" value="ocaciones"> En ocaciones</td><br></br>
    <td><input type="radio" name="colegiatura" value="siempre"> Siempre</td><br></br>
  </tr>
  <tr><br></br>
    <td>30.- Personas que dependan de ti economicante.</td><br></br>
    <td><input type="radio" name="dependan" value="familia"> Familia </td><br></br>
    <td><input type="radio" name="dependan" value="hijos"> Hijos </td><br></br>
    <td><input type="radio" name="dependan" value="nadie"> Nadie </td><br></br>
  </tr>
  <tr><br></br>
    <td>31.- ¿Vives con?</td><br></br>
    <td><input type="radio" name="vivir" value="padre"> Padre</td><br></br>
    <td><input type="radio" name="vivir" value="madre"> Madre</td><br></br>
    <td><input type="radio" name="vivir" value="ambos"> Ambos</td><br></br>
    <td><input type="radio" name="vivir" value="abuelos"> Abuelos</td><br></br>
    <td><input type="radio" name="vivir" value="tios"> Tíos</td><br></br>
    <td><input type="radio" name="vivir" value="esposa"> Esposa(o)</td><br></br>
    <td><input type="radio" name="vivir" value="solo"> Solo</td><br></br>
  </tr>
  <tr><br></br>
    <td>32.- ¿La casa don de vives es?</td><br></br>
    <td><input type="radio" name="casa" value="propia"> Propia</td><br></br>
    <td><input type="radio" name="casa" value="rentada"> Rentada</td><br></br>
    <td><input type="radio" name="casa" value="prestada"> Prestada</td><br></br>
  </tr>
  <tr><br></br>
    <td>33.- Número de hermanos.</td><br></br>
    <td><input type="radio" name="hermano" value="1"> 1 </td><br></br>
    <td><input type="radio" name="hermano" value="2"> 2 </td><br></br>
    <td><input type="radio" name="hermano" value="3"> 3 </td><br></br>
    <td><input type="radio" name="hermano" value="4"> 4 </td><br></br>
    <td><input type="radio" name="hermano" value="5"> 5 </td><br></br>
    <td><input type="radio" name="hermano" value="6"> 6 </td><br></br>
    <td><input type="radio" name="hermano" value="mas"> Más de 6. </td><br></br>
  </tr>
  <tr><br></br>
    <td>34.- Número de hermanos que cuentan con título universitario.</td><br></br>
    <td><input type="radio" name="hermanos" value="1"> 1 </td><br></br>
    <td><input type="radio" name="hermanos" value="2"> 2 </td><br></br>
    <td><input type="radio" name="hermanos" value="3"> 3 </td><br></br>
    <td><input type="radio" name="hermanos" value="4"> 4 </td><br></br>
    <td><input type="radio" name="hermanos" value="5"> 5 </td><br></br>
    <td><input type="radio" name="hermanos" value="6"> 6 </td><br></br>
    <td><input type="radio" name="hermanos" value="mas"> Más de 6. </td><br></br>
  </tr>
  <tr><br></br>
    <td>35.- Número de personas que viven en tu casa.</td><br></br>
    <td><input type="radio" name="personas" value="1"> 1 </td><br></br>
    <td><input type="radio" name="personas" value="2"> 2 </td><br></br>
    <td><input type="radio" name="personas" value="3"> 3 </td><br></br>
    <td><input type="radio" name="personas" value="4"> 4 </td><br></br>
    <td><input type="radio" name="personas" value="5"> 5 </td><br></br>
    <td><input type="radio" name="personas" value="6"> 6 </td><br></br>
    <td><input type="radio" name="personas" value="mas"> Más de 6. </td><br></br>
  </tr>
  <tr><br></br>
    <td>36.- ¿Quién solventa los gastos de casa?</td><br></br>
    <td><input type="radio" name="gastos" value="madre"> Madre</td><br></br>
    <td><input type="radio" name="gastos" value="padre"> Padre</td><br></br>
    <td><input type="radio" name="gastos" value="ambos"> Ambos</td><br></br>
    <td><input type="radio" name="gastos" value="yo"> Yo</td><br></br>
  </tr>
  <tr><br></br>
    <td>37.- Número de hermanos que actualmente estudian.</td><br></br>
    <td><input type="radio" name="herm" value="1"> 1 </td><br></br>
    <td><input type="radio" name="herm" value="2"> 2 </td><br></br>
    <td><input type="radio" name="herm" value="3"> 3 </td><br></br>
    <td><input type="radio" name="herm" value="4"> 4 </td><br></br>
    <td><input type="radio" name="herm" value="5"> 5 </td><br></br>
    <td><input type="radio" name="herm" value="6"> 6 </td><br></br>
    <td><input type="radio" name="herm" value="mas"> Más de 6. </td><br></br>
  </tr>
  <tr><br></br>
    <td>38.- ¿Realizas alguna actividad extracurricular?</td><br></br>
    <td><input type="radio" name="act" value="ninguna"> Ninguna </td><br></br>
    <td><input type="radio" name="act" value="deporte"> Deportes </td><br></br>
    <td><input type="radio" name="act" value="musica"> Musica </td><br></br>
    <td><input type="radio" name="act" value="baile"> Baile </td><br></br>
    <td><input type="radio" name="act" value="teatro"> Teatro </td><br></br>
  </tr>
  <tr><br></br>
    <td>39.- Relación con tus compañeros.</td><br></br>
    <td><input type="radio" name="relacion" value="mala"> Mala </td><br></br>
    <td><input type="radio" name="relacion" value="regular"> Regular</td><br></br>
    <td><input type="radio" name="relacion" value="buena"> Buena </td><br></br>
    <td><input type="radio" name="relacion" value="excelente"> Excelente </td><br></br>
  </tr>
    <tr><br></br>
    <td>40.- Discapacidad física</td> <br></br>
    <td><input type="radio" name="enfermedad" value="ninguna"> Ninguna</td><br></br>
    <td><input type="radio" name="enfermedad" value="visual"> Visual</td><br></br>
    <td><input type="radio" name="enfermedad" value="mental"> Mental</td><br></br>
    <td><input type="radio" name="enfermedad" value="motora"> Motora</td><br></br>
  </tr>
    <tr><br></br>
    <td>41.- Pasatiempo</td><br></br>
    <td><input type="radio" name="pasatiempo" value="ninguna"> Ninguno </td><br></br>
    <td><input type="radio" name="pasatiempo" value="videojuegos"> Videojuegos </td><br></br>
    <td><input type="radio" name="pasatiempo" value="musica"> Música </td><br></br>
    <td><input type="radio" name="pasatiempo" value="lectura"> Lectura </td><br></br>
    <td><input type="radio" name="pasatiempo" value="dibujos"> Dibujar </td><br></br>
    <td><input type="radio" name="pasatiempo" value="salir"> Salir de paseo. </td><br></br>
  </tr>
  <tr><br></br>
    <td>Evalua resultado: </td><br></br>
    <td><input type="submit" value="Evaluar"></td>
    <td></td>
  </tr><br></br>
  <h1>GRACIAS POR RESPONDER, TUS RESPUESTAS SERÁN PROCESADAS...</h1>
 
</body>
</html>
