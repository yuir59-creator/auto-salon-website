const cars = [
  {
    brand: 'Toyota',
    model: 'Camry 2021',
    body: 'Седан',
    engine: '2.5 л',
    transmission: 'АКПП',
    mileage: '45 000 км',
    price: 2950000,
    image: 'https://images.unsplash.com/photo-1552519507-da3b142c6e3d?auto=format&fit=crop&w=900&q=80'
  },
  {
    brand: 'Kia',
    model: 'Rio 2020',
    body: 'Хэтчбек',
    engine: '1.6 л',
    transmission: 'МКПП',
    mileage: '62 000 км',
    price: 1490000,
    image: 'https://images.unsplash.com/photo-1544636331-e26879cd4d9b?auto=format&fit=crop&w=900&q=80'
  },
  {
    brand: 'Hyundai',
    model: 'Tucson 2022',
    body: 'Кроссовер',
    engine: '2.0 л',
    transmission: 'АКПП',
    mileage: '32 000 км',
    price: 3150000,
    image: 'https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=900&q=80'
  },
  {
    brand: 'Volkswagen',
    model: 'Polo 2019',
    body: 'Хэтчбек',
    engine: '1.6 л',
    transmission: 'АКПП',
    mileage: '85 000 км',
    price: 1250000,
    image: 'https://images.unsplash.com/photo-1494905998402-395d579af36f?auto=format&fit=crop&w=900&q=80'
  },
  {
    brand: 'Toyota',
    model: 'RAV4 2023',
    body: 'Кроссовер',
    engine: '2.5 л',
    transmission: 'АКПП',
    mileage: '18 000 км',
    price: 4200000,
    image: 'https://images.unsplash.com/photo-1511919884226-fd3cad34687c?auto=format&fit=crop&w=900&q=80'
  },
  {
    brand: 'Kia',
    model: 'Sportage 2021',
    body: 'Кроссовер',
    engine: '2.0 л',
    transmission: 'АКПП',
    mileage: '41 000 км',
    price: 2890000,
    image: 'https://images.unsplash.com/photo-1553440569-bcc63803a83d?auto=format&fit=crop&w=900&q=80'
  }
];

const carsGrid = document.querySelector('#carsGrid');
const filterForm = document.querySelector('#filterForm');
const brandFilter = document.querySelector('#brandFilter');
const bodyFilter = document.querySelector('#bodyFilter');
const priceFrom = document.querySelector('#priceFrom');
const priceTo = document.querySelector('#priceTo');

function formatPrice(value) {
  return new Intl.NumberFormat('ru-RU').format(value) + ' ₽';
}

function renderCars(items) {
  carsGrid.innerHTML = '';

  if (!items.length) {
    carsGrid.innerHTML = '<div class="empty-state">По вашему запросу ничего не найдено.</div>';
    return;
  }

  items.forEach((car) => {
    const article = document.createElement('article');
    article.className = 'car-card';

    article.innerHTML = `
      <div class="car-img" style="background-image: linear-gradient(rgba(0,0,0,0.12), rgba(0,0,0,0.12)), url('${car.image}')">Фото авто</div>
      <div class="car-info">
        <div class="car-title">${car.brand} ${car.model}</div>
        <div class="car-specs">${car.engine}, ${car.transmission}, ${car.mileage}</div>
        <div class="car-price">${formatPrice(car.price)}</div>
        <button class="car-btn" type="button">Подробнее</button>
      </div>
    `;

    carsGrid.appendChild(article);
  });
}

function getFilteredCars() {
  const selectedBrand = brandFilter.value;
  const selectedBody = bodyFilter.value;
  const minPrice = Number(priceFrom.value) || 0;
  const maxPrice = Number(priceTo.value) || Number.MAX_SAFE_INTEGER;

  return cars.filter((car) => {
    const matchBrand = selectedBrand === 'all' || car.brand === selectedBrand;
    const matchBody = selectedBody === 'all' || car.body === selectedBody;
    const matchPrice = car.price >= minPrice && car.price <= maxPrice;
    return matchBrand && matchBody && matchPrice;
  });
}

filterForm.addEventListener('submit', (event) => {
  event.preventDefault();
  renderCars(getFilteredCars());
});

renderCars(cars);
