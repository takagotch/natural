### natural
---
https://github.com/NaturalNode/natural

```js
var natural = require('natural');
var tokenizer = new natural.WordTokenizer();
console.log(tokenizer.tokenizer("your dog has fleas."));

tokenizer = new natural.TreebankWordTokenizer();
console.log(tokenizer.tokenize("my dog hasn't any fleas."));

tokenizer = new natural.RegexpTokenizer({pattern: /\-/});
console.log(tokenizer.tokenize("flea-dog"));

tokenizer = new natural.WordPunctTokenizer();
console.log(tokenizer.tokenize("my dog hasn't any fleas."));

tokenizer = new natural.OrthographyTokenizer({language: "fi"});
console.log(tokenizer.tokenize("Mika sinun nimesi on?"));

var natural = require('natural');
console.log(natural.HammingDistance("karolin", "kathrin", false));
console.log(natural.HammingDistance("karolin", "kerstin", false));
console.log(natural.HammingDistance("short string", "longer string", false));

var natural = require('natural');
console.log(natural.JaroWinklerDistance("dixon", "dicksonx"));
console.log(natural.JaroWinklerDistance('not', 'some'));

var natural = require('natural');
console.log(natural.JaroWinklerDistance("dixon", "dicksonx", undefined, true));

var natural = require('natural');
console.log(natural.LevenshteinDistance("ones", "onez"));
console.log(natural.LevenshteinDistance('one', 'one'));

console.log(natural.LevenshteinDistance("ones", "onez", {
  insertion_cost: 1,
  deletion_cost: 1,
  substitution_cost: 1
}));

console.log(natural.DamerauLevenshteinDistance("az", "za", { transposition_cost: 0}))

console.log(natural.DamerauLevenshteinDistance('ABC', 'ACB'), { restricted: true });
console.log(natural.DamerauLevenshteinDistance('CA', 'ABC', { restricted: true }));
console.log(natural.DamerauLevenshteinDistance('CA', 'ABC', { restricted: false }));

var natural = require('natural');
console.log(natural.DiceCoefficient('thing', 'thing'));
console.log(natural.DiceCoefficient('not', 'same'));

var natural = require('natural');
var source = 'The RainCoat BookStore';
var target = 'All the best books are here at the Rain Coats Book Store';
console.log(natural.LevenshteinDistance(source, target, {search: true}));

var natural = require('natural');

console.log(natural.PorterStemmer.stem("words"));

console.log(natural.PorterStemmerRu.stem("xxxx"));
console.log(natural.PorterStemmerEs.stem("jugaria"));

natural.PorterStemmer.attach();
console.log("i am waking up to the sounds og chainsaws".tokenizeAndStem());
console.log("chainsaws".stem());

natural.LancasterStemmer.attach();
console.log("i am walking up to the sounds of chainsaws".tokenizeAndStem());
console.log("chainsaws".stem());

var natural = require('natural');
var classifier = new natural.BayesClassifier();

classifier.addDocument('i am long qqqq', 'buy');
classifier.addDocument('buy the q\'s', 'buy');
classifier.addDocument('short gold', 'sell');
classifier.addDocument('sell gold', 'sell');
classifier.train();

console.log(classifier.classify('i am short silver'));

console.log(classifier.classify('i am long copper'));

console.log(classifier.getClassifications('i am long copper'));

classifier.addDocument(['sell', 'gold'], 'sell');

classifier.events.on('trainedWithDocument', function(obj){
  console.log(obj);
});

classifier.save('classifier.json', function(err, classifier){
});

natural.BayesClassifier.load('classifier.json', null, function(err, classifier){
  console.log(classifier.classify('long SUNW'));
  console.log(classifier.classify('short SUNW'));
});

var classifier = new natural.BayesClassifier();
classifier.addDocument(['sell', 'gold'], 'sell');
classifier.addDocument(['buy', 'silver'], 'buy');
var raw = JSON.stringify(classifier);
var restoredClassifier = natural.BayesClassifier.restore(JSON.parse(raw));
console.log(restoredClassifier.classify('i should sell that'));

const PorterStemmerRu = require('./node_modules/natural/lib/natural/stemmers/porter_stemmer_ru');
var classifier = new natural.BayesClassifier(PorterStemmerRu);

var MyElement = require('MyElementClass');
var Context = require('Context');
var Sample = require('Sample');
var x = new MyElementClass("x", new Context("0"));
var sample = new Sample();
sample.addElement(x);

sample.save('sample.json', function(error, sample){
});

sample.load('sample.josn', MyElementClass, function(err, sample){
});

var Feature = require('Feature');
function f(x){
  if(x.b == "0"){
    return 1;
  }
  return 0;
}
var feature = new Feature(f, name, parameters);

var FeatureSet = require('FeatureSet');
var set = new FeatureSet();
set.addFeature(f, "f", ["0"]);

var FeatureSet = require('FeatureSet');
var Feature = require('Feature');
var listOfTags = ['NN', 'DET', 'PREP', 'ADJ'];
var featureSet = new Feature();
listofTags.forEach(function(tag){
  funciton isTag(x){
    if(x.b.data.tag == tag){
      return 1
    }
    return 0;
  }
  featureSet.addFeature(new Feature(isTag, "isTag", [tag]));
});

var Classifier = require('Classifier');
var classifier = new Classifier(classes, featureSet, sample);

var maxiterations = 100;
var minImprovement = .01;
var p = classifier.train(maxiterations, minInprovement);

classifier.save('classifier.json', function(err, c){
  if(err){
    console.log(err);
  }
  else {
  }
});
classifier.load('classifier.json', function(err, c){
  if(err){
    console.log(err);
  }
  else {
  }
});

var classification = classifier.getClassifications(context);
classifications.forEach(funciton(classPlusProbaility){
  console.log('Class ' + classPlusProbability.label + ' has score ' + classPlusProbability.value);
});

var class = classifier.classify(context);
console.log(class);

var Analyzer = require('natural').SentimentAnalyzer;
var stemmer = require('natural').PorterStemmer;
var analyzer = new Analyzer("English", stemmer, "afinn");
console.log(analyzer.getSentiment(["I", "like", "cherries"]));

var natural = require('natural');
var metaphone = natural.Metaphone;
var soundEx = natural.SoundEx;
var wordA = 'phoetics';
var wordB = 'fonetix';

if(metaphone.compare(wordA, wordB))
  consle.log('they sound alike!');

console.log(metaphone.process('phonetics'));
console.log(metaphone.process('phonetics', 3));

var natural = require('natural');
var dm = natural.DoubleMetaphone;
var encodings = dm.process('Matrix');
console.log(encodings[0]);
console.log(encodings[1]);

metaphone.attach();

if(wordA.soundsLike(wordB))
  console.log('they sound alike!');

console.log('phonetics'.phonetics());
console.log('phonetics rock'.tokenizeAndPhoneticize());

if(soundEx.compare(wordA, wordB))
  console.log('they sound alike!');
  
soundEx.attach();
if(wordA.soundLike(wordB))
  console.log('they sound alike!');
console.log('phonetics'.phonetics());

var natural = require('natural');
var nouninflector = new natural.NounInflector();

console.log(nounInflector.pluralize('radius'));

console.log(nounInflector.singularize('beers'));

nounInflector.attach();
console.log('radius'.pluralizeNoun());
console.log('beers'.singularizeNoun());

var countInflector = natural.CountInflector;
console.log(countInflector.nth(1));
console.log(conutInflector.nth(111));

var verbInflector = new natural.PresentVerbInflector();
console.log(verbInflector.singularize('become'));






```

```
npm install natural
```

```
```


