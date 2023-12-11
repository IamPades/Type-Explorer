## App.js

import React from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import MainPage from './components/MainPage/MainPage';
import ModelPage from './components/ModelPage/ModelPage';
import './App.css';

function App() {
return (
<Router>
<Switch>
<Route exact path="/" component={MainPage} />
<Route path="/models/:category" component={ModelPage} />
</Switch>
</Router>
);
}

export default App;

--- MainPage.js
import React from 'react';
import { useHistory } from 'react-router-dom';
import './MainPage.css';

function MainPage() {
const history = useHistory();

const navigateToCategory = (category) => {
history.push(`/models/${category}`);
};

return (
<div className="main-page">
<h1>Your Name - Your ID</h1>
<button onClick={() => navigateToCategory('flowers')}>Flowers</button>
<button onClick={() => navigateToCategory('trees')}>Trees</button>
<button onClick={() => navigateToCategory('cars')}>Cars</button>
</div>
);
}

export default MainPage;

--- ModelPage.js
import React from 'react';
import { useParams } from 'react-router-dom';
import ModelData from '../../models/ModelData';
import './ModelPage.css';

function ModelPage() {
const { category } = useParams();
const models = ModelData[category] || [];
const backgroundColor = {
flowers: 'blue',
trees: 'green',
cars: 'red',
};

return (
<div className="model-page" style={{ backgroundColor: backgroundColor[category] }}>
<h2>{category.toUpperCase()}</h2>
<ul>
{models.map((model, index) => (
<li key={index}>{model.name} - {model.info}</li>
))}
</ul>
</div>
);
}

export default ModelPage;

--- ModelData.js
const ModelData = {
flowers: [
{ name: 'Rose', info: 'Some basic information about Rose.' },
{ name: 'Sunflower', info: 'Some basic information about Sunflower.' },
{ name: 'Tulip', info: 'Some basic information about Tulip.' },
],
trees: [
{ name: 'Oak', info: 'Some basic information about Oak.' },
{ name: 'Maple', info: 'Some basic information about Maple.' },
{ name: 'Pine', info: 'Some basic information about Pine.' },
],
cars: [
{ name: 'Sedan', info: 'Some basic information about Sedan.' },
{ name: 'SUV', info: 'Some basic information about SUV.' },
{ name: 'Sports Car', info: 'Some basic information about Sports Car.' },
],
};

export default ModelData;

--- Component inside
import React from 'react';
function Button({ label, onClick }) {
return (
<button onClick={onClick}>
{label}
</button>
);
}

export default Button;

--- MainPage.css
.main-page {
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
height: 100vh;
}

.main-page button {
margin: 10px;
padding: 10px 20px;
font-size: 18px;
cursor: pointer;
}

--- ModelPage.css
.model-page {
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
height: 100vh;
color: white;
}

.model-page ul {
list-style: none;
padding: 0;
}

.model-page li {
margin: 5px 0;
}
